---
title: State Diagrams
---
(the raw `.drawio` file for these diagrams is in [State_Diagrams.drawio](uploads/1bf52741c4bd2b831263b7e086ef7dd5/State_Diagrams.drawio))

![diagram_under_maintenance.gif](uploads/72879fc112c8001ba2a6b8d01f065551/diagram_under_maintenance.gif){width="982" height="462"}

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

![State_Diagram_Overview.svg](uploads/ca7d031220240a86d7d9a63ae13d520a/State_Diagram_Overview.svg){width="1040" height="2019"}

> [!note]
>
> The "save game state and return to start" transition must be able to be done from all states within the placement and attack phase. I have explicitly left those transitions out of the detailed diagrams for those states as to not clutter the diagram too much.

## StartScreen Diagram

![State_Diagram_StartScreen.svg](uploads/c30db7f16f29fa5c7f9f629e58a02c0f/State_Diagram_StartScreen.svg){width="1018" height="445"}

## GameScreen Diagrams

### Placement Phase Diagram

![State_Diagram_Placement_Phase.svg](uploads/dcdfe0d874a015b54d398c57fd166ffc/State_Diagram_Placement_Phase.svg){width="1049" height="461"}

### Attack Phase Diagram

![State_Diagram_Attack_Phase.svg](uploads/146ce12b26c41711a8631e5bef6386ea/State_Diagram_Attack_Phase.svg){width="1041" height="737"}