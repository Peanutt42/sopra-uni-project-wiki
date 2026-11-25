---
title: Activity Diagrams
---
(the raw `.drawio` file is uploaded here: [Activity_Diagram.drawio](uploads/ee96291ed4f29a06b7db6a7f8ad6a025/Activity_Diagram.drawio))

![diagram_under_maintenance.gif](uploads/dffed83167ca3cd0fc2623cdd4bc7187/diagram_under_maintenance.gif){width="962" height="453"}

The activity diagrams should visualize the things a player can to do in the game, and in what order they can do those things.

For a more detailed, implementation focused diagram, see the State / Class diagrams.

![Activity_Diagram.svg](uploads/d9b9e7a45bead1bb9604201f2a63d623/Activity_Diagram.svg){width=1085 height=2679}

> [!note]
>
> Activity and State diagrams have somewhat of a overlap. This is both not too avoidable and is deliberate in order to cover all aspects of the games aspects.

## Main Menu and Game Selection

The game starts with the option for the player to quit, create a fresh game, load a exisiting game or open the help page.

Both loading and creating a game requires selecting a game save slot.

Creating a game in a game save slot means overriding the existing game in that slot.

## Ship placement

At the start of a fresh game, the player needs to place their ships. After a valid placement has been confirmed, the enemy AI places its ships and the game can go over to the AttackPhase that forms the main game loop.

## Main game loop

At the start of a round, the game can be saved and the player can go back to the `StartScreen` or continue playing the next round.

The game determines who can play first, human or AI player.

When the human player is at their turn, they have to pick a tile to attack next. They can continue to attack a enemy tile until their attack has missed (has not hit any enemy ships). After both players had their turn, the next round starts.

The game checks the win condition after every kind of attack on tiles/ships and can therefore transition to the GameOver/EndScreen when all ships of a player have been sunken.

The game shows the outcome and the statistics with a option to go back to the GameScreen.

## Lightning Event

On top of normal player attacks on tiles/ships, there is the lightning event that strikes on random tiles. When the Lightning server is enabled and available it can determine where a lightning might strike. This can too trigger a win condition.
