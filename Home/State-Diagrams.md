---
title: State Diagrams
---
(the raw `.drawio` file for these diagrams is in [State_Diagrams.drawio](uploads/ac4116f1dbb7113f90f2865f77dcfd37/State_Diagrams.drawio))

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

![State_Diagram_Overview.svg](uploads/9276a71c92b23668772921a22786d8cd/State_Diagram_Overview.svg){width=1012 height=2232}

> [!note]
>
> The "save game state and return to start" transition must be able to be done from all states within the placement and attack phase. I have explicitly left those transitions out of the detailed diagrams for those states as to not clutter the diagram too much.

## StartScreen Diagram

![State_Diagram_StartScreen.svg](uploads/65c0242ccd73cdd23b0b7d9c79b02d3c/State_Diagram_StartScreen.svg){width=1017 height=386}

## GameScreen Diagrams

### Placement Phase Diagram

![State_Diagram_Placement_Phase.svg](uploads/02a06016576e89737beb112ebfc2674c/State_Diagram_Placement_Phase.svg){width=1055 height=463}

### Attack Phase Diagram

![State_Diagram_Attack_Phase.svg](uploads/a4b10a2a5d4d89f94d34358909fac5ab/State_Diagram_Attack_Phase.svg){width=1034 height=732}