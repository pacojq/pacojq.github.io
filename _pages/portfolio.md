---
title: "Portfolio"
excerpt: "Portfolio"
sitemap: false
permalink: /portfolio/


gallery-pjrp:
  - url: /assets/images/projects/pjrp/image_001_0000.png
    image_path: /assets/images/projects/pjrp/image_001_0000.png
    title: "Screenshot of sample scene rendered in Unity with PJRP."

gallery-deckrx:
  - url: /assets/images/games/deck-rx/image_022_0000.png
    image_path: /assets/images/games/deck-rx/image_022_0000.png
    title: "Screenshot of a race in Deck RX."
  - url: /assets/images/games/deck-rx/tutorial.jpg
    image_path: /assets/images/games/deck-rx/tutorial.jpg
    title: "Screenshot of Deck RX's tutorial race."

gallery-texwriter:
  - url: /assets/images/projects/texwriter/example.png
    image_path: /assets/images/projects/texwriter/example.png
    title: "Xaloc Editor."
  - url: /assets/images/projects/texwriter/noise.png
    image_path: /assets/images/projects/texwriter/noise.png
    title: "Screenshot of an example noise texture generated with TexWriter."

gallery-xaloc:
  - url: /assets/images/projects/xaloc/sandbox-editor.png
    image_path: /assets/images/projects/xaloc/sandbox-editor.png
    title: "Xaloc Editor."
  - url: /assets/images/projects/xaloc/sandbox.png
    image_path: /assets/images/projects/xaloc/sandbox.png
    title: "Screenshot of an example application built with Xaloc."
    
gallery-tools:
  - url: /assets/images/portfolio/tools_chapter-editor.png
    image_path: /assets/images/portfolio/tools_chapter-editor.png
    title: "Example node editor view of a main quest for a chapter in a narrative game."
  - url: /assets/images/portfolio/tools_rosetta.png
    image_path: /assets/images/portfolio/tools_rosetta.png
    title: "Rosetta: in-house localization tool."
  - url: /assets/images/portfolio/tools_dialogue-editor.png
    image_path: /assets/images/portfolio/tools_dialogue-editor.png
    title: "Very simple dialogue view in the node-based editor."
  - url: /assets/images/portfolio/tools_ignited-font-scanner.png
    image_path: /assets/images/portfolio/tools_ignited-font-scanner.png
    title: "Ignited Steel toolset: Localization asset scanner."
  - url: /assets/images/portfolio/tools_map-editor.png
    image_path: /assets/images/portfolio/tools_map-editor.png
    title: "Hexagonal tile level editor, modifying enemy spawn areas."
  - url: /assets/images/portfolio/tools_ignited-mesh-sandwitch.png
    image_path: /assets/images/portfolio/tools_ignited-mesh-sandwitch.png
    title: "Ignited Steel toolset: 'Sandwiched' sprite stack mesh generator."

gallery-graphics:
  - url: /assets/images/projects/path-tracer/out.png
    image_path: /assets/images/projects/path-tracer/out.png
    title: "Simple C++ renderer with software-based path tracing."
  - url: /assets/images/games/deck-rx/GIF 29-10-2021 12-27-17.gif
    image_path: /assets/images/games/deck-rx/GIF 29-10-2021 12-27-17.gif
    title: "Deck RX car outlines and environment VFX."
  - url: /assets/images/portfolio/vulkan-renderer.png
    image_path: /assets/images/portfolio/vulkan-renderer.png
    title: "Vulkan Renderer. Japanese mask by Romain Vaysse, under CC Attribution-NonCommercial license."
  - url: /assets/images/portfolio/roman-mosaic.png
    image_path: /assets/images/portfolio/roman-mosaic.png
    title: "Roman mosaic. Early splash screen for Songs of Steel: Hispania."
  - url: /assets/images/portfolio/acorn.png
    image_path: /assets/images/portfolio/acorn.png
    title: "Screen capture of an RPG prototype with volumetric lighting."
  - url: /assets/images/portfolio/custom-srp-01.jpg
    image_path: /assets/images/portfolio/custom-srp-01.jpg
    title: "PBR lighting in a custom Render Pipeline for Unity."

    
gallery-talks:
  - url: /assets/images/portfolio/talk-idd.jpg
    image_path: /assets/images/portfolio/talk-idd.jpg
    title: "Me (right), giving a talk at IndieDevDay conference in Barcelona."

---

Feel free to check out my [GitHub account](https://github.com/pacojq) for an overview of my public programming work.
For a detailed view of my professional experience, please refer to my <a href="https://www.linkedin.com/in/paco-juan-6589ba14b/">LinkedIn profile</a>.


## Graphics & Tech Art

- **PJRP.** PBR render pipeline built from scratch in C# for Unity, fully working in PC, Nintendo Switch, Xbox Series X/S PlayStation 4 and PlayStation 5. <a href='https://github.com/pacojq/PJRP'>[Source Code]</a> <i class='fab fa-github' />

{% include gallery id="gallery-pjrp"  %}

- **[Deck RX](https://store.steampowered.com/app/1529180/Deck_RX_The_Deckbuilding_Racing_Game/).** Developed the game as Graphics Programmer and Tech Artist. Work in this project includes:
  - Modification and extension of Unity's URP forward renderer to add deferred features,
  - Toon-like illumination and fullscreen outline effect,
  - Environment fog and lighting for every world,
  - In-game special effects and particles

{% include gallery id="gallery-deckrx"  %}


- **[Ignited Steel](https://store.steampowered.com/app/1550740/Ignited_Steel_Mech_Tactics/).** Designed and implemented a "Sprite Stack" based render pipeline, which achieves a pixelated 3D graphic effect using animated layers of 2D sprites.
- **Path Tracer.** Simple renderer following Peter Shirley's book ["Ray Tracing in One Weekend"](https://raytracing.github.io/books/RayTracingInOneWeekend.html). <a href='https://github.com/pacojq/RayTracingInOneWeekend'>[Source Code]</a> <i class='fab fa-github' />
- **Vulkan Renderer.** Small project used to learn Vulkan. <a href='https://github.com/pacojq/HelloVulkan'>[Source Code]</a> <i class='fab fa-github' />
- **Project Attrah.** Procedural world generation module, relying on compute shader programs and multi-threaded processes. Transforming a flat world to give it a \textit{round planet} look via vertex manipulation. Vertices displaced with a HLSL shader, running in real-time at 60 Hz.

{% include gallery id="gallery-graphics"  %}



## Engine Programming

- **Xaloc.** A 2D game engine written in C++. It's an engine with an ECS approach, that supports OpenGL rendering and allows C# scripting through mono. <a href='https://github.com/pacojq/Xaloc'>[Source Code]</a> <i class='fab fa-github' />

{% include gallery id="gallery-xaloc"  %}


## Tools Programming

- **TexWriter.** A shader-based image genrator, built using C++, OpenGL and ImGui. <a href='https://github.com/pacojq/TexWriter'>[Source Code]</a> <i class='fab fa-github' />

{% include gallery id="gallery-texwriter"  %}

- **Rosetta.** Proprietary localization tool written in C++, using XML, OpenGL and ImGui. Used for the game localization process in Meteorbyte Studios releases. Provides basic functionality, such as basic project statistics, text search and filtering, content preview with different fonts and character sets, and string comparison among different languages.
- **Buildbot Fork.** Used Python and [Buildbot](https://buildbot.net/) to develop an internal Continuous Integration tool, which automates PC and PS4 builds.
- **_Deck RX_ Toolset.** Tile-based level editor for in-game circuits. Programmed as a standalone C# Unity application and outputting level data in both JSON and binary file formats.
- **_Ignited Steel_ Toolset.** Multiple Unity extensions and custom tools for the development of the console versions of the game, including: 
  - A "sprite stack" mesh generator, which allows the preview and generation of sliced mesh assets from a given set of sprites,
  - A Localization Scanner, with the ability of checking the whole asset database looking for unlocalised UI elements or miss-configured font asset references.
- **_Songs of Steel: Hispania_ Toolset.** Designed and implemented multiple key tools in asset creation pipeline for _[Songs of Steel](https://store.steampowered.com/app/2603300/Songs_of_Steel_Hispania/)_, a narrative strategy game. Among them:
  - Node-based editor for Narrative Designers to structure both quests and dialogue assets in Unity,
  - In-engine hexagonal tilemap editor, allowing the modification of navmeshes, level terrain conditions, trigger areas and enemy spawn zones.
- **Unity extensions.** Vast work in custom Unity tools and extensions for the Unity Editor, to deliver the best-fitting toolset for artists and designers' needs in each project.

{% include gallery id="gallery-tools"  %}


## Bachelor Thesis

A Narrative Engine for video games with parallel and open storytelling.

Built as a core module in [_Project Attrah_](https://pacojq.github.io/games/attrah),
its initial design and achitecture proposal was awarded [Most Innovative Cultural Project](https://www.culturaydeporte.gob.es/en/cultura/industriasculturales/mejores-proyectos/modernizacion-2019.html) 
of the year by the Ministry of Culture and Sports.

It has been used in the narrative strategy game _[Songs of Steel: Hispania](https://store.steampowered.com/app/2603300/Songs_of_Steel_Hispania/)_,
as the core system to handle the story events of the campaign.

### Abstract

We have developed a multi-platform Narrative Engine which can help a video
game build a story with different levels of developer and player authorship.
We have accomplished this by abstracting all narrative occurrences that make
the plot advance to different kind of Events, which can be triggered after
internal changes of the game state. In addition, our system presents other
sort of narrative utilities, such as Characters with different sets of skills and
attributes, and multiple approaches to the way the previous-mentioned events
are triggered, like Affairs that bind our internal system state to the game’s
state or Event Pools, which will trigger events over time based on arbitrarily
set priorities. Our system is currently being used by multiple in-development
commercial projects.


## Other Work

- **Talks and conferences.** Experience talking to broader audiences, both as a University
guest lecturer and as a speaker in game conferences.

{% include gallery id="gallery-talks"  %}

- **steam2xml.** Small command line program to transform Steam achievement files from VDF to XML. <a href='https://github.com/pacojq/steam2xml'>[Source Code]</a> <i class='fab fa-github' />
- **ChromeTracing.NET.** A C# visual profiling library using Google Chrome's [tracing](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool) tool. <a href='https://github.com/pacojq/ChromeTracing.NET'>[Source Code]</a> <i class='fab fa-github' />
- **Seagull.** Toy programming language, compiling to intermediate language. Targeting MAPL Virtual Machine, an academic virtual machine built at University of Oviedo. The compiler is developed in C#, with the help of ANTLR for lexical and syntax analysis.<a href='https://github.com/pacojq/Seagull'>[Source Code]</a> <i class='fab fa-github' />
- **DeChat.** A decentralized chat web application using [_Solid_](https://solid.inrupt.com). Developed as a team project with other students from the Software Engineering Degree at Universidad de Oviedo. <a href='https://github.com/Arquisoft/dechat_en1a'>[Source Code]</a> <i class='fab fa-github' />
