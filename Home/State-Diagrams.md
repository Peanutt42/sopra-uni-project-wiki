---
title: State Diagrams
---
(the raw `.drawio` file for these diagrams is in [State_Diagrams.drawio](uploads/ac4116f1dbb7113f90f2865f77dcfd37/State_Diagrams.drawio))

Links to the different state diagrams:

* [Overview](#overview-diagram)
* [StartScreen](#startscreen-diagram)
* [GameScreen](#gamescreen-diagrams)
  * [Placement Phase](#placement-phase-diagram)
  * [Attack Phase](#attack-phase-diagram)

## Explanation

The state diagram(s) show the different states the game can be in.

They should be more towards the technical side of the implementation.

User flow / how the user interacts with the game is better described by the [Activity Diagrams](./Activity-Diagrams).

## Overview Diagram

![State_Diagram_Overview.svg](uploads/9276a71c92b23668772921a22786d8cd/State_Diagram_Overview.svg){width="1012" height="2232"}

> [!note]
>
> The "save game state and return to start" transition must be able to be done from all states within the placement and attack phase. I have explicitly left those transitions out of the detailed diagrams for those states as to not clutter the diagram too much.

The game starts with loading the configuration file, checking if the file exists and is corrupt. Additionally the game checks whether the confguration is valid. If the configuration does not exist, is corrupt or invalid, a default configuration is loaded instead.

After that, the `StartScreen` is started. From there the player can get to the `GameScreen` or the `HelpPage`.

The `GameScreen` consists of two phases: `PlacementPhase` and `AttackPhase`.

After that screen, the game transitions to the `EndScreen`.

## StartScreen Diagram

![State_Diagram_StartScreen.svg](uploads/65c0242ccd73cdd23b0b7d9c79b02d3c/State_Diagram_StartScreen.svg){width="1017" height="386"}

The `StartScreen` is the first loaded Screen and is the state from where and where most of the screen transitions happen. For example in order to go to the settings or help screen while in a active game in the `GameScreen`, the user must first go to the `StartScreen`. This ensures that that the game state is properly saved and does not need to be handled at every possible state within all screens.

## GameScreen Diagrams

### Placement Phase Diagram

![State_Diagram_Placement_Phase.svg](uploads/02a06016576e89737beb112ebfc2674c/State_Diagram_Placement_Phase.svg){width="1055" height="463"}

The `PlacementPhase` does not transition until the ship placmenet is valid and confirmed or the game is paused and saved. The user can place unplaced ships, move/rotate/remove placed ships from the board field. After a valid placment is confirmed, the phase transitions to the `AttackPhase`.

### Attack Phase Diagram

![State_Diagram_Attack_Phase.svg](uploads/a4b10a2a5d4d89f94d34358909fac5ab/State_Diagram_Attack_Phase.svg){width="1034" height="732"}

The `AttackPhase` consists of multiple rounds. At the start of each round the game requests the thunder event and attacks the chosen tiles (or skips when not available yet). After that if the win condition has not yet been met, the game determines what player gets to play their turn first. When their turn is over (and the win condition has not yet been met), the other player has their turn and the round is over, starting a new round if the win condition has not yet been met.

Once the win condition is met, the game transitions to the `EndGameScreen`.