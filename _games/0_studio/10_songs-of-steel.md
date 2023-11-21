---
title: "Songs of Steel"
layout: single
permalink: /games/songs-of-steel
share: false

excerpt: "Graphics & Core programmer [2020-23, in dev]"
post_type: "Studio Projects"

header:
  teaser: /assets/images/games/songs-of-steel/capsule.png

sidebar:
  - image: /assets/images/games/songs-of-steel/capsule.png
    image_alt: "Songs of Steel: Hispania cover art"
    
  - title: "Platforms"
    text: "<i class='fab fa-steam'></i> [Steam](https://store.steampowered.com/app/2603300/Songs_of_Steel_Hispania/)"

  - title: "About"
    text: "**Genre**: Strategy, turn-based. <br>
    **Players**: Singleplayer.<br>
    **Engine**: Unity.<br>
    **Role**: Core programmer, Graphics programmer, Technical Artist"
    
gallery:
  - url: /assets/images/games/songs-of-steel/screenshot-tutorial.jpg
    image_path: /assets/images/games/songs-of-steel/screenshot-tutorial.jpg
    #alt: "placeholder image 1"
    title: "Screenshot of a battle in the game's campaign."
  - url: /assets/images/games/songs-of-steel/FcryxcUWYAMHelp.jpg
    image_path: /assets/images/games/songs-of-steel/FcryxcUWYAMHelp.jpg
    #alt: "The classic Sponza scene, rendered with Songs of Steel's graphic pipeline."
    title: "The classic Sponza scene, rendered with Songs of Steel's graphic pipeline."
  - url: /assets/images/games/songs-of-steel/FPGd5BHXoAQq-HZ.jpg
    image_path: /assets/images/games/songs-of-steel/FPGd5BHXoAQq-HZ.jpg
    #alt: "placeholder image 3"
    title: "Test decal in an empty level."

---

_Songs of Steel: Hispania_ is an up-coming PC game, for which I have
contributed in a range of core and graphics programming tasks, and some
remarkable work under the role of tech artist.

### Tools Programming

Designed and implemented multiple key tools in asset creation pipeline for the game. Among them:
  - Node-based editor for Narrative Designers to structure both quests and dialogue assets in Unity,
  - In-engine hexagonal tilemap editor, allowing the modification of navmeshes, level terrain conditions, trigger areas and enemy spawn zones,
  - In-engine grass brush tool, for populating levels with procedurally-generated grass geometry.

### Graphics Programming and Tech Art

The game has a custom deferred Render Pipeline, extending the capabilities of Unity's 
default URP forward renderer, presenting a custom toon lighting model that tries
to match a comic style similar to the one found in Mike Mignola's works.

Also, technical art work is present in a variety of forms, as:
  - Tree foliage shader,
  - Volumetric snow effect for cold environments,
  - Colored mask for occluded characters,
  - Level decal system,
  - and others.

{% include gallery caption="Songs of Steel: Hispania visual style and graphics." %}

### Other Responsibilities

Other notable work in this project can list as:
 
 - Design and implementation of a level and asset loading pipeline.
 - UI programming and effects.
 - Game settings and save system.
 - Navigation AI and path-finding for units and individual models.

### Release information

 - **PC (Steam)**: TBD.
