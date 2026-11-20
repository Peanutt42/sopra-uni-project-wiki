---
title: Home
---
## Introduction

This is the wiki of the game "Sopra versenken - Ship happens". The purpose of this wiki is to include implementation details like diagrams as well as help and tutorials for the hole game including the UI and the game's rules.

This here is the **Home** which gives a general overview of what the game is about and where to find different implementation details.

## General Description

"Sopra versenken - Ship happens" is a local single-player (potentially local two-player) strategy game based on "Schiffe versenken".

The player plays against an algorithm that has the same information and abilities as the player.

First in the placement phase each player places all of their ships on a fixed grid of square tiles. Both board fields are the same size and at the start each player cannot see anything about the enemy's board placement.

Then in the attack phase, each player chooses one tile of the enemy board to attack and gets feedback whether that attack hit a ship or not. The player who first sinks all ships of the enemy before their own ships are sunk wins the game.

## Screens

### StartScreen

The first screen shown after launching the game application. it offers game save slots that can be loaded / can be used to create a fresh game. Additionally the user can go to the SettingsScreen, HelpScreen or quit the game completely.

### GameScreen

The GameScreen has two phases: placement and attack phase.

The two board fields are always visible but only the own tiles and ships are all visible, the enemy's are only revealed if hit or sunk.

The currently ongoing game can always be saved and the user can go back to the StartScreen.

In the attack phase, there is a chance that tiles might get attacked by a thunder.

### EndScreen

Shows who won the game, the number of rounds, what and how many ships were each sunk, how many lightning events etc.

No action can be done in this Screen, the user can only go back to the StartScreen.

### SettingsScreen

Exposes configurable settings that are saved in a configuration file.

### HelpScreen

## System Restrictions and Dependencies

The detailed dependencies and how to compile and run the game are described in detail in the `README.md`. Still, here is a quick overview of the supported platforms and different ways of compiling and running the game:

The game can be compiled on Linux and Windows (MacOS should work but has not yet been tested).

The easiest way to compile and develop the game on Linux is using [nix](https://nixos.org/download/).

The game can run on both Wayland and X11 when on Linux. The game additionally runs in a WebGL/webgpu supporting browser using WASM (like Firefox or Chromium based browsers). The browser build is the simplest when just trying to run the game.

## Mood board

The mood board can be found [here](./Home/Mood-board). It contains many screenshots and references to technical presentations, game-dev talks and reference implementations of mostly graphical rendering features.

## Diagrams

### [State Diagrams](./Home/State-Diagrams)

### [Activity Diagrams](./Home/Activity-Diagrams)

### [Class Diagrams](./Home/Class-Diagrams)