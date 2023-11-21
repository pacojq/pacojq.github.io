---
title: "Introducing Xaloc Engine"
permalink: /posts/introducing-xaloc-engine

excerpt: "Introducing Xaloc Engine."

header:
  #image: /assets/images/posts/2020-02-05-hello-world/teaser.jpg
  #teaser: /assets/images/posts/2020-02-05-hello-world/teaser.jpg
categories:
  - Devlog
tags:
  - Xaloc
  - Game Engine
  - Devlog
  - Programming
---

> Introducing Xaloc Engine: yet another 2D game engine developed in C++.

So, for the last two months I've been working on a small project in my spare ime, which
is starting to look like an *actual thing*: the [**Xaloc game engine**](https://github.com/pacojq/Xaloc).

![Screenshot of an example application built with Xaloc.](/assets/images/posts/2020-07-03-introducing-xaloc-engine/sandbox.png){: .align-center}

I've been toying around with the idea of developing my own engine for some time, mostly
for learning porpuses. While I have some years of experience in developing video games,
I've always been more interested in the technology behind them.

Through small experiments in Java, C# or JavaScript, trying both 2D and 3D rendering, I've
got myself into the *ancient art of crafting engines*™ -should be said, of course, that
these projects just gave me a teeny tiny idea of how an *actual* engine works.

However, the "discovery" of the [Hazel Engine](https://github.com/TheCherno/Hazel) development
[video series](https://www.youtube.com/watch?v=JxIZbV_XjAs&list=PLlrATfBNZ98dC-V-N3m0Go4deliWHPFwT)
turned to be the prefect excuse to finally deep dive in the world of game engine development.

Dear reader, may I introduce Xaloc Engine.


## The Engine

As I've mentioned above, the development of Hazel Engine -huge shout out to its creator, 
[Yan Chernikov](https://twitter.com/thecherno)-, was the reason I started this project.

The Hazel series' episodes -by date June 2020- have been an immense source of 
learning, and they have set a great starting point por a game engine development.
So, even though I've already added to the engine a bunch of code of my own, most of the
codebase so far is shared with the Hazel project.

This said, let's take a look at Xaloc.


### Overview and Objectives

Xaloc is a 2D game engine, and this simplifies **a lot** of stuff. 

Getting rid of the 3D part allows me to forget about rendering techniques which are 
*completely* out of scope, and focus on the fundamentals.

Thus, my objectives with this project are the following:

  - **Architecture.** Learning how to design a small game engine. How all parts should fit 
  and communicate with each other.
  - **Rendering.** Getting familiar with how a renderer works, including render passes and
  pipelines.
  - **Asset management.** Learning how an engine handles assets, such as textures, audio files,
  localization data, etc. 
  - **ECS**. Although I don't really want to deep dive on this one, I want Xaloc running
  with the closest I can get to an Entity-Component-System approach. [entt](https://github.com/skypjack/entt) 
  is a good starting point.
  - **Multi-platform development.** Have Xaloc running in Windows, Linux and Mac. While I've got a bunch of experience in languages such as C#, Java of JavaScript, they all have huge trait in common: they're platform-agnostic.
  With Xaloc, I want to learn how to develop a native application which can run in different
  platforms.
  - **Rendering APIs.** I'm putting this one at the very end because it's maybe the most
  *ambitious* of my objectives -and, one could argue, out of scope. I want to have Xaloc as
  an excuse to learn how to program targetting multiple render APIs, starting with OpenGL and
  Vulkan, and maybe continuing with DirectX in a -quite distant- future.


### Engine Structure

Xaloc has a very simple structure, which divides the game in layers. Each layer -defined by
the own Engine or by the actual game- defines its own behaviour on every frame update,
on rendering and -if necessary- on rendering debug utilities with [ImGui](https://github.com/ocornut/imgui).

Whenever a layer wants to render something, it will call the Renderer -*duh*. The renderer,
which is completely static, provides an abstract interface for whatever rendering API we're
using -right now, OpenGL.

Even though the Engine is meant to be used to develop 2D games, the renderer fully supports
3D geometry. This feature will come in handy in the future, when the game editor will be
able to provide a three-dimensional debug view of the scene.

And, now that we've got game logic running in layers and some nice textures being rendered,
we need things interacting with each other in the screen -otherwise, we would be playing 
quite a boring game. Here's when entities appear.


### Scenes and Entities

Every time I've had to develop a *game-engine-like* program, I've faced it in an object-oriented
way. You know, we have the `GameObject` class, some references to `Component` objects inside, 
`SpriteRenderer`, `Collider`, etc. all inheriting from `Component`... you know the drill.

With Xaloc I wanted to change the approach and go data-oriented, and use an 
*Entity–Component–System* (ECS) to excecute game logic -to know the benefits of ECS, go listen to [Mike Acton](https://www.youtube.com/watch?v=rX0ItVEVjHc), he really knows what he's talking about. 

The task of transitioning to ECS has been extremely easy, thanks to [entt](https://github.com/skypjack/entt).
With this library, Entities -the equivalent to the old GameObjects- are just an ID that bind 
their components together when needed. 

The rest of the time, we can perform the game logic by simply iterating through the desired 
component types -which are *just data*- and excecuting small, straight-forward operations on them.

To put all this together, scenes control when and which operations are done with the data
from the components, and provide a tiny interface so we can create and destroy
entities and components.


### Scripting

One of my main objectives with this project was to learn how engines use scripting languages.

And -because I love to make my life more difficult- Lua wasn't "enough". Even though Lua is
a very popular and easy-to-implement scripting language, I *really* love C#. Like, a lot. And
I knew it was possible to [embed it using mono](https://www.mono-project.com/docs/advanced/embedding/scripting/), 
so I decided to give it a try.

As a result, Xaloc provides a very simple C# API -*extremely* simple in comparison with the
native C++ API-, which allows transform manipulations and some operations with components.
Here you can see an example of how to make a *two-minute* player controller in C#.

![Programming player movement in C#.](/assets/images/posts/2020-07-03-introducing-xaloc-engine/csharp-demo.gif){: .align-center}


## The Editor

In addition to the mentioned above, Xaloc also has its own editor. Right now it's, quite 
bare-bones -even more than the actual Engine.

However, it has a nice game preview viewport, a scene hierarchy view, and a property editor.
These three things alone can already help a lot if you want to build a good-looking scene.

Also, they provide enough content to attach to this post a beautiful screenshot of the 
Xaloc Editor.

![Screenshot the Xaloc editor with a simple sandbox game.](/assets/images/posts/2020-07-03-introducing-xaloc-engine/xaloc-editor.png){: .align-center}


## Future work

As one may notice, the current state of the Engine is far from accomplishing the objectives I
mentioned previously. A lot of work still needs to be done, and the roadmap looks something 
like this:

**BASIC OBJECTIVES**

- **Audio.** Like, come on, this one is quite basic.
- **Font and UI rendering.** It would be great to be able to write stuff that the player could read.
- **Physics system.** This will most probably provide a very basic collision API, just like 
[GameMaker Studio's](https://docs.yoyogames.com/source/dadiospice/002_reference/movement%20and%20collisions/collisions/index.html). 
I really like how simple and yet powerful that API is.

**ADVANCED OBJECTIVES**

- **Vulkan support.** So we can have multiple rendering APIs, as mentioned in the *Objectives*
section above.
- **Asset manager.** Integrated with the editor, so we can listen to changes in the file system, change the source file an asset is pointing to, etc.
- **Play / Edit mode.** So we can "execute" the game without exiting the editor.

To keep an eye on the most recent changes in the engine, check the 
[development branch](https://github.com/pacojq/Xaloc/tree/dev) on the GitHub repo!