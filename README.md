# public-notes
Public notes about the development process and how Fuchsia runs internally.

## Fuchsia Plugin Structure
```
PaperMC Server
├── [O] Gaura - Plugin framework/api for its children, used by all of our Paper plugins.
|   ├── [O] Circaea - Permissions plugin handling permissions for each player and group.
|   |
|   └── [C] Taraxia - Core plugin containing network wide features such as rank displaying, friends, whispering, database, player tab, boss bar.
|       ├── [C] Lopezia - Lobby plugin managing player interactions, lobby NPCs, parkour, etc.
|       |
|       ├── [C] Eulobus - Events plugin managing week long events, running async with eachother in different worlds. Also handles event groups and such.
|       |   ├── [C] Capture-the-flag event, handling specific stats, logic, etc for it.
|       |   └── [C] ...any other events.
|       |
|       └── [C] Megacorax - Minigames plugin handling duel minigames running async with eachother in different worlds, as well as parties and queuing, etc.
|           ├── [C] No-Debuff Duels, handling specific stats, logic, etc for it.
|           ├── [C] Boxing Duels, handling specific stats, logic, etc for it.
|           ├── [C] Classic Duels, handling specific stats, logic, etc for it.
|           ├── [C] Sumo Duels, handling specific stats, logic, etc for it.
|           ├── [C] Top Fight Duels, handling specific stats, logic, etc for it.
|           ├── [C] Bridge Duels, handling specific stats, logic, etc for it.
|           └── [C] ...any other minigames.
|
└── [O] Clarkia - Velocity plugin handling sending players to lobbies and proxy restarts.

[O] - Open sourced
[C] - Close sourced
[U] - Undecided
```
