# BioHazard

> A 2D top-down survival game developed in **C++ and Qt** as an academic software engineering project.

<img width="395" height="331" alt="titlemenu" src="https://github.com/user-attachments/assets/daa96c96-fa7a-4a4c-b34b-0f7219cb5d94" />

## Overview

**BioHazard** is a 2D top-down survival game built with **C++ and Qt Widgets**.

The player must survive successive waves of enemies while navigating a map containing obstacles, damaging surfaces and areas with different movement characteristics.

The project was developed as an academic exercise to apply concepts of **object-oriented programming, data structures, algorithms, event-driven programming and basic game development**.

## Trailer

https://www.youtube.com/watch?v=Mn0KQ3iGBPY

---

## Features

* 2D top-down player movement
* <img width="16" alt="mutant" src="https://github.com/user-attachments/assets/92400270-e8cd-4358-a780-71aff7ab94e1" /> Wave-based enemy spawning
* <img width="16" height="16" alt="laser" src="https://github.com/user-attachments/assets/cf97bb9b-1070-425d-a3fe-5b7126ad671a" /> Directional projectile system
* <img width="16" height="16" alt="UL2" src="https://github.com/user-attachments/assets/bdd045cc-9e1a-4889-b809-becf51a9b3e8" /> Sprite-based character animation
* Tile-based map representation
* <img width="16" alt="ammo" src="https://github.com/user-attachments/assets/6109203c-90a2-4d01-a3b8-f1f6058b7e58" /> Collision detection with map obstacles and collectable items
* Enemy navigation using a vector-field approach
* Damage zones
* Surfaces with movement friction and enemies with physics-based movement
* <img width="16" height="16" alt="healer" src="https://github.com/user-attachments/assets/c78c9443-6678-4a44-bde0-c7f2d14fd82c" /> Player health system
* <img width="16" alt="icon" src="https://github.com/user-attachments/assets/61202ba8-82b2-4c9e-81d4-72594de6d7fe" /> Progressive enemy difficulty across waves
* Victory and defeat conditions

---

## Technical Overview

### Technology Stack

| Technology              | Purpose                                |
| ----------------------- | -------------------------------------- |
| **C++**                 | Core application and game logic        |
| **Qt**                  | GUI, graphics scene and event system   |
| **Qt Widgets**          | Application interface                  |
| **QGraphicsScene**      | 2D game world                          |
| **QGraphicsView**       | Rendering and camera                   |
| **QGraphicsPixmapItem** | Player sprite                          |
| **QTimer**              | Game loops, movement and animation     |
| **Qt Resource System**  | Embedded game assets                   |
| **qmake**               | Project configuration and build system |

---

## Enemy Navigation

One of the main technical components of BioHazard is the enemy navigation system.

The game represents the map as a **24 × 40 grid of nodes**. Each node stores information about its position, accessibility, neighbors and distance from the player's current position.

Each node can have up to eight neighboring nodes, allowing movement in cardinal and diagonal directions.

### Distance Map

When the player moves, the game generates a distance map starting from the player's current node.

A **breadth-first search (BFS)** approach is used to propagate distances through the traversable nodes.

Conceptually:

```text
Player
  ↓
[0] [1] [2] [3]
[1] [1] [2] [3]
[2] [2] [2] [3]
```

The resulting distances are then used to determine the direction an enemy should follow.

### Vector Field

After calculating the distance map, each node receives a normalized direction vector pointing toward a neighboring node with a smaller distance.

This creates a **vector field across the map**.

Enemies can therefore determine their movement direction based on the vector associated with the node they currently occupy.

<img width="480" alt="VF" src="https://github.com/user-attachments/assets/7d0aea4f-fd43-415e-96da-b98d07b80f46" />

This approach allows multiple enemies to navigate toward the player without requiring an independent path calculation for every enemy.

---

## Game Architecture

The project is organized around several C++ classes representing the main entities and systems.

```text
game
│
├── player1
│   └── Player movement, animation and health
│
├── enemy
│   └── Enemy behavior and movement
│
├── bullet
│   └── Projectile behavior
│
├── nodo
│   └── Map node and navigation data
│
├── obstaculo
│   └── Map obstacles
│
└── vec3
    └── Vector operations
```

The Qt graphics framework is used as the foundation for the interactive game scene.

---

## Project Structure

The original internal project structure is intentionally preserved so that the project can be opened and built using its existing **qmake** configuration.

```text
BioHazard/
│
├── BioHazard.pro
├── resources.qrc
│
├── *.cpp
├── *.h
├── *.ui
│
├── MOV/
│   └── Character sprite sheets
│
├── BGI/
│   └── Background and map images
│
└── 2D/
    └── Additional graphical and audio assets
```

The source files remain in the project root because this reflects the original Qt project structure and ensures that the existing resource paths and build configuration remain functional.

---

## Gameplay

The game is structured around successive enemy waves.

Each wave increases the number and/or characteristics of the enemies. Different levels introduce additional difficulty through changes in enemy damage, mass, speed and movement behavior.

### Gameplay Loop

```text
Player input
     ↓
Player movement
     ↓
Update navigation field
     ↓
Enemy direction calculation
     ↓
Enemy movement
     ↓
Collision / damage
     ↓
Wave progression
```

<img width="480" height="" alt="demo1opt" src="https://github.com/user-attachments/assets/f7c1fc49-57de-4851-a5e0-1134acbd0ae8" />

<img width="480" height="" alt="demo2opt" src="https://github.com/user-attachments/assets/2b3b2ddc-c4cc-4492-aac9-1ca2487ee977" />


---

## Screenshots

### Gameplay

<img width="480" alt="maingp" src="https://github.com/user-attachments/assets/2d34435d-5a32-4d8f-b35f-84fe0a7294aa" />

### Map

<img width="480" alt="escenario" src="https://github.com/user-attachments/assets/14dcc509-a2ca-4b32-9f41-d58d399a88a7" />

### Secondary Combat Mechanics

<img width="480" alt="maingp2" src="https://github.com/user-attachments/assets/fb251247-26d6-45ee-943f-88835918ea9c" />

---

## Building and Running

### Requirements

* **Qt Creator**
* A compatible **Qt installation**
* A C++ compiler supported by the selected Qt version
* `qmake`

### Using Qt Creator

1. Clone or download this repository.
2. Open `BioHazard.pro` with **Qt Creator**.
3. Select an appropriate Qt kit and compiler.
4. Configure the project.
5. Build the project.
6. Run the application.

The project uses Qt's resource system, so the graphical assets referenced by `resources.qrc` are included as part of the project.

> **Note:** This repository contains the source project and its available resources. Some assets from the original academic build were removed because their redistribution rights could not be verified.

---

## Academic Context

BioHazard was developed as an **academic project** to apply programming and software development concepts in a practical application.

The project explores topics including:

* Object-oriented programming
* C++ classes and inheritance
* Event-driven programming
* Data structures
* Breadth-first search
* Graph-based navigation
* Vector mathematics
* Collision detection
* Animation
* GUI and graphics programming

---

## Project Status

**Completed academic project.**

The project is functional and represents the state of the software at the time of its original development.

It contains known limitations and implementation issues typical of an academic project. The repository preserves the original implementation rather than presenting it as a production-ready game.

---

## Credits & Assets

BioHazard combines original work from the development team with graphical assets obtained from external sources during development.

The development team does **not claim ownership of third-party assets**. Original work created by the team and externally sourced material are distinguished below.

### Original Assets

The following elements were created, edited or assembled by the development team:

* `2D/laser.png`
* Player and gameplay graphics created specifically for the project
* Interface elements created for the project
* Background compositions and level layouts in `BGI/`
* Original graphical compositions assembled using external tiles
* Other project-specific graphical elements not identified as third-party assets below

The final compositions and level layouts in `BGI/` were created by the development team, although some of their underlying graphical tiles originate from the third-party **Ashlands Tileset** described below.

---

### Third-Party Assets

#### Ammunition Icon

`2D/ammo.png`

Source: **Flaticon**
Author: **Smashicons**
License: Attribution required

Attribution provided by the original source:

> Bala icons created by Smashicons - Flaticon

Source: https://www.flaticon.es/icono-gratis/balas_222861

#### Healer / Health Icon

`2D/healer.png`

Source: **PNGWing**

The source page indicates that the material is available for **non-commercial use**. The original author or creator could not be identified from the available source information.

Source: https://www.pngwing.com/es/free-png-vfjca

This asset is retained in the repository as part of the original academic project.

#### Enemy Spaceships

`2D/Ship.png`
`2D/Ship2.png`

Source: **CraftPix.net — Free Pixel Art Enemy Spaceship 2D Sprites**

The assets were obtained through the free download provided by CraftPix.net. According to the source page, the free download grants **royalty-free usage in unlimited projects**.

Source: https://craftpix.net/freebies/free-pixel-art-enemy-spaceship-2d-sprites/

#### Industrial Background

`2D/city.gif`

Source: **OpenGameArt — Industrial Parallax Background**
Author: **ansimuz**
License: **CC0**

The original background was obtained from OpenGameArt and subsequently edited for use in BioHazard.

Source: https://opengameart.org/content/industrial-parallax-background

The version included in the project is an edited adaptation of the original asset.

#### Ashlands Tileset

`BGI/escenario.png`
`BGI/escenario2.png`

The environments used in BioHazard were assembled by the development team using tiles from the **Ashlands Tileset**.

Source: **FinalBossBlues — Ashlands Tileset**
Author: **FinalBossBlues**

The asset page describes the tileset as a free release and states that **commercial use is permitted and attribution is not required**.

Source: https://finalbossblues.itch.io/ashlands-tileset

The individual tiles were arranged, edited and composed by the development team into the final scenario images used by the game.

---

### Removed Assets

Some assets from the original academic build were intentionally removed from this repository because their copyright status or redistribution rights could not be sufficiently verified.

The removed assets include:

* `AUD/00.mp3` — copyrighted music from the *Monolith Official Soundtrack*, track *Fire in the Hole* by ArcOfDream
* `MOV/mutant.png` — sprite from *Alien Massacre*, originally obtained through The Spriters Resource
* `MOV/` character sprites based on *MERCS*
* `2D/track1.mp3` — original source and licensing could not be reliably verified
* `2D/laser.mp3` — original source and licensing could not be reliably verified

These files are **not included in the repository**.

Their removal means that the repository version may not contain every asset present in the original academic build.

---

### Asset Attribution

The development team has attempted to identify and properly attribute externally sourced assets used during development.

Where an original source could not be reliably identified, the corresponding asset was removed from the repository rather than being presented as original work.

The repository therefore distinguishes between:

* **Original work** created by the development team
* **Third-party assets** used according to their available terms
* **Removed assets** whose redistribution rights could not be sufficiently verified

---

### Third-Party Libraries

BioHazard uses the **Qt framework**.

Qt official website: https://www.qt.io/

---

## Development

**Language:** C++
**Framework:** Qt
**Build system:** qmake
**Project type:** Desktop 2D game
**Context:** Academic project

---

## Development Team

**Santiago Giraldo**
Electronics Engineering student · Universidad de Antioquia

**Sebastian Bonilla**
Electronics Engineering student · Universidad de Antioquia

---

> **Note:** This repository preserves the original academic implementation of BioHazard. Its purpose is to document the project, its technical concepts and the development work involved. Third-party assets remain the property of their respective authors and copyright holders.
