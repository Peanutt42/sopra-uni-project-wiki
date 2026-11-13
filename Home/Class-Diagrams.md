---
title: Class Diagrams
---
(the raw `*.drawio` file is uploaded to: [Class_Diagrams.drawio](uploads/dcb2df5611eefe3f4e8d276911fa0797/Class_Diagrams.drawio))

The main idea while designing was to try and follow the principle of single source of truth.

That means that rather than multiple states storing the same or equivalent information, the information is stored in one place and referenced everywhere else.

One important example of this is the board field information, so what tiles have been hit, whether a ship is on that tile and whether a ship has been sunken on that tile. While storing this information in the BoardState and in the Ship would be easy, it could introduce states where the board and the ship do not agree with each other, resulting in bugs that are very hard to trace back and find their root issue. 

## ThunderEvent

![Class_Diagram_ThunderEvent.svg](uploads/98912c8a092b3affa028e5eb6bafa0a1/Class_Diagram_ThunderEvent.svg){width="1048" height="1223"}

## Configuration File

![Class_DIagram_ConfigurationFile.svg](uploads/61c39f1ca578e8495ffc2f0022248c6a/Class_DIagram_ConfigurationFile.svg){width="998" height="1050"}

## Game Saving

![Class_Diagram_GameSaving.svg](uploads/9d071d2dbbae086eeb328ce56a5dd643/Class_Diagram_GameSaving.svg){width="1042" height="1676"}

## Screens

![Class_Diagram_Screens.svg](uploads/16603d36e7dd1a644bea7a8aa4a30db3/Class_Diagram_Screens.svg){width="1052" height="1499"}

In order for faster iteration speed while experimenting and developing the game, the game engine has a hot-reloading feature that optionally loads all game code as a dynamically loaded shared library that can be removed and swapped out. This requires the game engine to transition the game's state which also means that the game engine needs a way to serialize and deserialize the game's state in a way that does not require binary compatibility.

Importantly, this serialization is only meant for hot-reloading while developing and not for saving/loading the game's state to resume later, as the serialization/deserialization needed for hot-reloading requires storing much more information about the game's state's types and structure.

The save and resume game later mechanic is separate of that game engine feature.

## Domain

![Class_Diagram_Domain.svg](uploads/44fc2a036f92d2cfd4827bc5fbf18329/Class_Diagram_Domain.svg){width="1074" height="744"}