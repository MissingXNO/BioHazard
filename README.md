# BioHazard

> A 2D top-down survival game developed in **C++ and Qt** as an academic software engineering project.

![BioHazard gameplay placeholder](assets/screenshots/gameplay-placeholder.png)

## Overview

**BioHazard** is a 2D top-down survival game built with **C++ and Qt Widgets**.

The player must survive successive waves of enemies while navigating a map containing obstacles, damaging surfaces and areas with different movement characteristics.

The project was developed as an academic exercise to apply concepts of **object-oriented programming, data structures, algorithms, event-driven programming and basic game development**.

---

## Features

* 🎮 2D top-down player movement
* 🧟 Wave-based enemy spawning
* 🔫 Directional projectile system
* 🎞️ Sprite-based character animation
* 🗺️ Tile-based map representation
* 🧱 Collision detection with map obstacles
* 🧭 Enemy navigation using a vector-field approach
* 🔥 Damage zones
* 🧊 Surfaces with movement friction
* ❤️ Player health system
* 📈 Progressive enemy difficulty across waves
* 🏆 Victory and defeat conditions

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

```text
        N
    NW  │  NE

W ──────●────── E

    SW  │  SE
        S
```

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

![Vector field placeholder](assets/screenshots/vector-field-placeholder.png)

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
└── BGI/
    └── Background and map images
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

![Gameplay GIF placeholder](assets/gifs/gameplay-placeholder.gif)

---

## Screenshots

### Gameplay

![Gameplay screenshot](assets/screenshots/gameplay-01.png)

### Map

![Map screenshot](assets/screenshots/map-01.png)

### Combat

![Combat screenshot](assets/screenshots/combat-01.png)

> **TODO:** Replace these placeholders with screenshots from the actual running application.

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

Game assets and external resources used by the project are documented here.

### Assets

| Asset             | Source / Author     | License     |
| ----------------- | ------------------- | ----------- |
| Character sprites | `[SOURCE / AUTHOR]` | `[LICENSE]` |
| Background / map  | `[SOURCE / AUTHOR]` | `[LICENSE]` |
| Other assets      | `[SOURCE / AUTHOR]` | `[LICENSE]` |

> **TODO:** Complete this section after verifying the origin and licensing of each asset.

### Third-Party Libraries

BioHazard uses the **Qt framework**.

[Qt official website](https://www.qt.io/)

---

## Development

**Language:** C++
**Framework:** Qt
**Build system:** qmake
**Project type:** Desktop 2D game
**Context:** Academic project

---

## Repository

Source code and project resources:

[GitHub Repository](PLACEHOLDER_REPOSITORY_URL)

---

## Author

**[YOUR NAME]**

[LinkedIn](PLACEHOLDER_LINKEDIN_URL) · [GitHub](PLACEHOLDER_GITHUB_URL)

---

> **Note:** This repository preserves the original academic implementation of BioHazard. Its purpose is to document the project, its technical concepts and the development work involved.
