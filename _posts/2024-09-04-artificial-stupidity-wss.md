---
layout: post
title: "Artificial Stupidity in World Soccer Strikers '91"
subtitle: "designing a soccer AI that simply does the trick"
post_type: "post"
seoTitle: "Artificial Stupidity in World Soccer Strikers 91"

header-img: "img/posts/2024-09-04-artificial-stupidity-wss/background.png"
header-mask: 0.7

categories:
  - posts
tags:
  - world-soccer-strikers
  - artificial-intelligence
  - programming
  - game-design
---

[_World Soccer Strikers '91_](/games/world-soccer-strikers-91)
is an **arcade soccer game**, with a high
focus on local multiplayer gameplay. I started developing it in 2020,
right after COVID-19 hit, and we all were forced to stay at home for a
good bunch of weeks.

Some of the key elements of this game are its **palpable arcade spirit**,
or the **unique gameplay physics**, where the ball is its own physical
object, and bounces around totally decoupled from the bodies of the players
on the field. However, from all the different design aspects of the game,
one of the more **complex, fun to develop, and crucial to hit**, was the
AI for the CPU-controlled players.

And I say _complex_ without meaning it was technically challenging, or
that the AI needed a specially intricate behaviour. Rather, AI for this
game needed to be **as stupid as possible**, without reaching the point
of being disruptive to the Player's experience.

> As a small note, the word **player** is used a lot in this article,
> to refer to the characters that appear in the game, running around and
> doing soccer stuff. To avoid confusion when mentioning the actual person
> who's playing the game, we are going to refer to the latter as the **Player**,
> with a capital **P**.


## _World Soccer Strikers_' AI model

_World Soccer Strikers '91_ makes use of **two different structures** to
model the behaviour of the AI-controlled players in the game. The first, a
high-level [State Machine](https://gameprogrammingpatterns.com/state.html);
the second, a more specific set of [Behaviour Trees](https://www.gamedeveloper.com/programming/behavior-trees-for-ai-how-they-work)
for both goalkeepers and field players. Let's take a deeper look.


### general states

On a high-level, the AI that controls the players works with a state
machine, tightly bound to the overall flow of a match in _World Soccer
Strikers_. Said State Machine defines the following states:

 - **In-Game.** The players are actively participating in the match,
 and executing the corresponding AI logic, depending on whether they
 play in a goalkeeper or field position, and whether they are in the
 Player's team or not.

 - **Goal Scored.** If their team scores, players will run around the
 pitch, celebrating. It's a pretty silly state that picks random points
 that players can run towards, while a whole UI sequence plays in the
 foreground.

 - **Goal Received.** While players in the other team celebrate, players
 in the team that received the goal will stand still, playing an idle
 animation with a defeated look. This state also lasts for the duration
 of the "goal scored" UI sequence.

 - **Match End.** In a very similar fashion to the previous two states,
 as players will celebrate and run around if they've won the match. The
 only addition is that they will remain with a standard idle animation
 in case of a tied match.

 - **Transition.** This is a utility state, utilized to transition to
 another arbitrary state, only with an extra time delay. While said
 transition is running, the player will appear to be in a sort of an
 inactive state.

 - **User Controlled.** The final state we define is a sort of a fake
 state, where no AI code is execute. When a character is controlled by
 a Player, **the received input is treated as AI actions** that we then
 send for execution, in the same way as other AI states in this State
 Machine do.

{% include post-image.html src="/img/posts/2024-09-04-artificial-stupidity-wss/celebration.jpg" description="change of state after a goal - capture courtesy of <a href='https://www.devuego.es/bd/fjuego/world-soccer-strikers-91'>DeVuego</a>." %}

Something to mention regarding the high-level State Machine is that it
does not include any sort of implementation for automatic transitions.
Every jump to a different state is _manually_ and explicitly triggered
in different parts of the gameplay code.

Should the model were more complex than it actually ended up being, this
decision might, indeed, not have been the wisest. However, this solution
turned out to be a pretty good option, that **just does the trick**, and,
due to the simplicity of the gameplay needs, most of the alternatives would
have been a complete over-kill for readability and maintainability of the
code.


### behaviour trees

Behaviour Trees are a data structure that is composed of different kinds
of nodes, connected in the shape of a tree, that will be evaluated in a
[depth-first](https://en.wikipedia.org/wiki/Depth-first_search) manner.

Although many types of nodes can be used in a video game AI, _World Soccer
Strikers_ utilizes the **three minimum ones that _every_ Behaviour Tree needs
to define**, plus an extra utility node for convenience. They list as
follow:

 - **Action Node**. Executes an action, which can take an arbitrary amount
 of time to complete. Every update tick, we execute the code in this action
 node and evaluate whether the current state is a `Success`, this is, we
 completed the task without any inconvenience; whether we might still be
 `Running` the action; or if, alternatively, the execution was a `Failure`.

 - **Sequence Node**. Stores a list of child nodes, and executes them. When
 the current active child executes successfully, it will start updating the
 next sibling. In case a failure state was returned, the execution would
 stop and run again, starting from the first child.

 - **Selector Node**. Works similarly to the Sequence Node, with the
 difference being that the Selector will try to update all its children,
 one after the other, until we find the first sibling that does _not_ fail
 to execute.

 - **Wait Node**. This last one is an utility node, that will just wait for
 an arbitrary amount of seconds until it succeeds. It can come in handy when
 adding cool-downs between actions in Sequence Nodes.

To illustrate how this would work, here's a small example of how a goalkeeper's
Behaviour Tree looks (omitting the logic inside the tree action nodes).

```csharp
BehaviourTree BuildBT()
{
  return new BehaviourTreeBuilder(_keeper)
    .Sequence("behaviour")
      .Selector("defence")
        .Sequence("jump-sequence")
            .Do("jump", t => BT_Jump())
            .WaitSeconds("wait", _jumpTime)
            .Do("stop", t =>
            {
              _mov = Vector2.zero;
              return BehaviourTreeStatus.Success;
            })
        .End()
        .Do("keep-in-bounds", t => BT_KeepPlayerInBounds())
        .Do("follow-ball",    t => BT_FollowBallMovement())
      .End()
      .WaitSeconds("wait", bt_updateTime)
    .End()
  .Build();
}
```

## goalkeeper AI

As one might guess from the code above, goalkeepers have -by far- **the simplest
behaviour** among AI-controlled players in the game.

Their activity is limited to moving around, in-bounds, trying to follow the
ball and, if they reckon it's a good chance to do so, jump and try to stop it.

It's worth mentioning that their behaviour includes some tweaks to add some
_flavour_ to gameplay. For example, jump speed and cool-downs will change
depending on match difficulty; and some constrains are applied to the jumping
actions, preventing the goalkeeper to jump forward and invade the Player's
space.


## field player AI

Now, if we talk about field players, _World Soccer Strikers_' AI makes all of
them take part in both offensive and defensive duties -except for some exceptions
that we will mention later in this article.

While this behaviour is considerably more complex than a goalkeeper's, we try
to **stick to the general simplicity of the gameplay**, and have a very reduced set
of key decision points for AI-controlled field players.

Some of the most important checks in the Behaviour Tree when the player is
attacking are:

 - **_Does a teammate have the ball?_** If so, do not disturb them. Try to
 maintain position or getting open to receive a pass.

 - **_Is any rival next to me?_** If a player has control of the ball, the main
 question that will determine which actions to take is whether there's any rival
 nearby. If the path is free, we will try to **get the best look at the goal** as
 possible, and shoot to score. However, in the case of being next to an opponent,
 the options will be reduced to **attempting a dribbling move or passing the ball**
 to an open teammate.

Meanwhile, on defense we can find a decision tree that kinda mirrors the
one we just described:

 - **_Am I near the ball?_** Try to get between it and the goal. If possible,
 clear it in the opposite direction from the defending goal.

 - **_In my team, Am I the closest to the ball?_** Run towards it, with a
 strong preference of getting in front of it. If we evaluate we have a nice
 chance, tackle the opponent -as the move will get us closer to the ball too.

 - **_Is the goal unprotected?_** While the default instruction for defenders
 is to keep position if there's a teammate trying to engage with the ball,
 all of them will run to **cover the defending goal** if the attacker has a clear
 line of sight. When the goal is protected by another teammate, the player
 will be able to go back to their original position.

As an extra consideration, there might be moments of the match in which
two players are fighting for control of the ball, thus, possession is not
totally in favour of either team.
For this specific cases, players that are not engaging in that fight take
a sort of **minimalistic branch** in their Behaviour Trees, that tries to
ensure that: everyone maintains their position in the field, away from
the ball, so that **we are not adding fuel to the fire**; and we try to make
sure that there's at least one player protecting the goal, in case the
fight for possession ends in a random shot.


## player senses

Now, all these decisions that the AI must make have to be **bound to the
actual state of the match** -otherwise, anything of what we've mention would
make much sense-. That's why _World Soccer Strikers_' players have an
extra component to define their _senses_.

{% include post-image.html src="/img/posts/2024-09-04-artificial-stupidity-wss/player-senses.png" description="trigger areas for player senses." %}

In this game, we call _senses_ the set of inputs that the AI will receive
to **make the most adequate decision every frame**. And, although the list is
not too long, it does more than enough to give us the data that we need
to evaluate the tactical situation of a player. They function in the
following way:

 - **Ball control area.** Region where, should the ball be in this range,
 the player can interact with it. This is, shooting it, passing to a
 teammate, or attempting a dribble move. It applies regardless of whether
 the player is in the attacking or defending team.

 - **Opponent influence area.** This area is also used to check for close
 teammates. This way -taking back the example from the previous section-,
 we can avoid situations in which two players of the same team try to
 engage with the ball at the same time.

 - **"Near ball" area.** This last region defines whether a player is in
 range to be considered "next to the ball". Apart from determining
 several decisions in the players' Behaviour Trees, it's also used to
 resolve which team has control of the ball.

 - **Distance to goal.** From the -very few, actually- field positioning
 metrics that players hold, the distance to the goal might be the most
 relevant. As we implemented a heavy bias to prevent players from kicking
 far goal attempts, this distance turns out to be the one of the main
 factors dealing with the behaviour of an attacker.

 - **Line of sight.** As opposed to the previous metric, this one is used
 for **both offense and defense**. In the case of an attacking player, they
 will check their own line of sight towards the goal with the objective of
 finding an open look to shoot the ball; when that player is defending,
 though, they will check the line of sight **of their opponent**, to know
 whether they should run to cover the defending goal.



## team tactics

Another point of discussion is how these individual behaviours we've
described work and organize together as a team. And actually... in
the case of _World Soccer Strikers_, we don't worry much about this
topic.

As we dealing with a multiplayer-first, party game, we took the
decision of **reducing team tactics to their minimal expression**: the
team formation.

{% include post-image.html src="/img/posts/2024-09-04-artificial-stupidity-wss/formation.jpg" description="initial kick-off of a match, where we can clearly see the two formations the teams are adopting." %}

With this approach, each team can have a go-to layout that **defines
the preferred position** for each AI-controlled player. And, to spice
things up a little bit, higher difficulty levels also define a
**special behaviour** for players that end up in a [_winger_](https://en.wikipedia.org/wiki/Winger_(sports))
or _backer_ role -although this special case for AI only applies in
_Player vs CPU_ matches.

This turned out to be a pretty good call, as these formations give
personality to each team in the game, and invite the Player to try
different things with every new opponent.


## swapping players

As a finishing note, a common question in cases like this is: **what if
the Player wants to swap characters** and take control of an AI-controlled
player?

Well, in _World Soccer Strikers_ this was not really an issue, as the
question was solved in a **pretty natural, straight-forward way**: as 
mentioned before in this article, we consider "controlled by Player" to
be just another AI state. In the end, from the high-level view, that's
just a black box that, after an update tick, tells the player where to
move and whether it should pass or shoot the ball.

This approach simplifies the whole swapping players feature, converting
it in **a mere change of state**. When the Player swaps again and the AI
re-takes control, the in-game state resets and starts executing again.
Just as if we were coming from, for example, a "goal received" state.
