---
title: Class Diagrams
---
(the raw `*.drawio` file is uploaded to: [Class_Diagrams.drawio](uploads/aacac21c0efe33a1f607e1b385b33e99/Class_Diagrams.drawio))

![diagram_under_maintenance.gif](uploads/4983fc35379ab1db3f7471690bc7d22f/diagram_under_maintenance.gif){width="984" height="463"}

The main idea while designing was to try and follow the principle of single source of truth.

That means that rather than multiple states storing the same or equivalent information, the information is stored in one place and referenced everywhere else.

One important example of this is the board field information, so what tiles have been hit, whether a ship is on that tile and whether a ship has been sunken on that tile. While storing this information in the BoardState and in the Ship would be easy, it could introduce states where the board and the ship do not agree with each other, resulting in bugs that are very hard to trace back and find their root issue.

## ThunderEvent

![Class_Diagram_ThunderEvent.svg](uploads/0cc0767f936226f584dd25ace24ddce0/Class_Diagram_ThunderEvent.svg){width="998" height="1169"}

## Configuration File

![Class_DIagram_ConfigurationFile.svg](uploads/c4f2c8d970402d3d4658626c5e497285/Class_DIagram_ConfigurationFile.svg){width="1119" height="1216"}

## Game Saving

![Class_Diagram_GameSaving.svg](uploads/52243ba0c6884630ea8b756a3c9bd664/Class_Diagram_GameSaving.svg){width="976" height="1727"}

## Screens

![Class_Diagram_Screens.svg](uploads/7bffd974e604f91aa1d55fc7427b6d4d/Class_Diagram_Screens.svg){width="991" height="1733"}

In order for faster iteration speed while experimenting and developing the game, the game engine has a hot-reloading feature that optionally loads all game code as a dynamically loaded shared library that can be removed and swapped out. This requires the game engine to transition the game's state which also means that the game engine needs a way to serialize and deserialize the game's state in a way that does not require binary compatibility.

Importantly, this serialization is only meant for hot-reloading while developing and not for saving/loading the game's state to resume later, as the serialization/deserialization needed for hot-reloading requires storing much more information about the game's state's types and structure.

The save and resume game later mechanic is separate of that game engine feature.

## Domain

![Class_Diagram_Domain.svg](uploads/4a7750074242c85c3a8e6021c737b424/Class_Diagram_Domain.svg){width=1066 height=741}