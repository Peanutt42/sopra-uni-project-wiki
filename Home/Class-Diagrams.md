---
title: Class Diagrams
---
(the raw `*.drawio` file is uploaded to: [Class_Diagrams.drawio](uploads/aacac21c0efe33a1f607e1b385b33e99/Class_Diagrams.drawio))

![diagram_under_maintenance.gif](uploads/4983fc35379ab1db3f7471690bc7d22f/diagram_under_maintenance.gif){width="984" height="463"}

The class diagrams are split into separate topics: Domain, Configuration file, Game saving, Screens and the Thunder event.

The main idea while designing was to try and follow the principle of single source of truth.

That means that rather than multiple states storing the same or equivalent information, the information is stored in one place and referenced everywhere else.

One important example of this is the board field information, so what tiles have been hit, whether a ship is on that tile and whether a ship has been sunken on that tile. While storing this information in the BoardState and in the Ship would be easy, it could introduce states where the board and the ship do not agree with each other, resulting in bugs that are very hard to trace back and find their root issue.

## Domain

![Class_Diagram_Domain.svg](uploads/4a7750074242c85c3a8e6021c737b424/Class_Diagram_Domain.svg){width=1066 height=741}

The domain class diagram has a few domain specific classes. They are keep track of the game state (phase, round, board states of both players, player at turn, game over, etc.). The ships and tile state get handled by this class. The most important parts of the `ShipGame` class is the `attackTile()` method that returns a `AttackResult` and the `getTileState()` method for checking the state of a single tile. The `ShipGame` enables the principle of single source of truth, since multiple parts of the game need to know different parts of the games state, but storing the information for all of those separately would lead to dublication which then can lead to different values for the same information of the games state.

The enum `AttackResult` has all possible outcomes of a tile getting attacked (by player or by thunder). `TileState` is the enum representing all possible states of a tile.

The `AIStrategy` interface allows for defining and testing multiple versions of a enemy AI algorithm. It also makes it easy to define a prototype/mock AI enemy that just chooses randomly in order to develop other parts of the game before having to have developed all the other parts of the game. The `AIStrategy` can then use `getTileState` from the perspective of the AI enemy to get only the information that a normal human player would also have access to.

## Configuration File

![Class_DIagram_ConfigurationFile.svg](uploads/c4f2c8d970402d3d4658626c5e497285/Class_DIagram_ConfigurationFile.svg){width="1119" height="1216"}

The `GameConfig` class represents all configuration values from the saved JSON configuration file. It must be loaded and validated from the relative filepath. It contains things like the WS-URL, round at which the thunder event can happen (optional) and also the board size (width + height). There must also be a fixed default `GameConfig`.

The `ShipConfig` class has all the information needed to describe a ship type, like how many of the ship type have to be placed. The type of the ship can have four predefinied values: `Explorer`, `Cruiser`, `Mothership` or `Custom`. How a custom ship type will be specified in the configuration file will be determined later on in the development.

When ships are placed on the board, they can have four orientations: `Normal`, `CW90`, `CW180`, `CW270` (CW = __C__ ounter-clock- __W__ ise). This is needed in order to support asymmetric ship designs later on.

## Game Saving

![Class_Diagram_GameSaving.svg](uploads/52243ba0c6884630ea8b756a3c9bd664/Class_Diagram_GameSaving.svg){width="976" height="1727"}

`SaveGameManager` owns all at least 3 `SaveGameSlot`s. It handles creating, deleting and loading these `SaveGameSlot`s.

The `SaveGameSlot` class holds all needed information for load the game state back to a equivalent state where each part of the game state that is gameplay related is loaded back exactely how it was when saving in order to not change the games outcome.

This information includes the current `GamePhase`, current round, current `Player` and both players `BoardState`.

The `BoardState` stores the attacked tiles and the `Ship`s on that board.

## Screens

![Class_Diagram_Screens.svg](uploads/7bffd974e604f91aa1d55fc7427b6d4d/Class_Diagram_Screens.svg){width="991" height="1733"}

The Screens diagram shows how the custom game engine and the game code interact, and how the game code separates into different `Screen`s.

The game engine creates a small interface to communicate with the game, that includes updating the games state and inspecting it. The interface is kept small in order to minimize the leakage of game engine code and game logic code.

This enables hot-reloading only the game logic code that has changed while the game engine keeps running by loading the game logic code as a dynamically loaded shared library. That is also why keeping the `GameApi` interface small is important.

There can only be one `Screen` active in a `Game`. `Game` also owns the `GameConfig`.

A `Screen` can be updated, returning a potential new `Screen` to transition to and be rendered using the game engines `Renderer`. The rendering should have the `Screen` itself as a immutable reference, meaning that the `Screen` cannot change its state while rendering.

The different `Screen`s that need to be implemented are:

- `StartScreenState`: starts new games, quits or opens the help and settings screens.
- `GameScreenState`: handles the entire active gameplay using the `ShipGame` class.
- `EndScreenState`: handles the overview after a finished `GameScreenState`
- `HelpScreenState`: shows the help page
- `SettingsScreenState`: allows for changing game settings in the game.

The `GameStats` class should contain all needed information for the `EndScreenState` to show a overview of the finished game. This is needed as the state of the active `ShipGame` in the `GameScreenState` gets destroyed when transitioning to the `GameScreenState`.

## ThunderEvent

The `ThunderService` handles everything related to owning the WebSocket connection as well as processing the responses of the WS-Server and rolling them out on the game. The `WebSocketClient` is a placeholder for a external library for handling the lower level networking of WebSockets.

The JSON request and response protocoll is represented by the `LightningRequeset` and `LightningResponse` classes that contain all the fields of the JSON payloads. Ideally they should have a proc-macro auto generate the serialization and deserialization logic to JSON for easier validation and less boilerplate code.
