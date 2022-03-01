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

## PaperMC Server Naming Scheme
*Todo: Cool diagram!*

#### `name` `spigot server id`-`server instance id`

**For example:**

`lobby1-A` - 1st PaperMC server dedicated to lobbies, connected to the first lobby instance on that PaperMC server.  
- 1 lobby PaperMC server supports 3 lobby instances, each housing 50 players.

`event6-D` - 6th PaperMC server dedicated to events, connected to the 4th event instance on that PaperMC server.  
- 1 event PaperMC server *generally* supports 4 event instances, each housing 40 players.
- Players per event is able to dynamically change, and thus change the amount of instances able to be ran on that PaperMC server.

`minigame12-AB` - 12th PaperMC server dedicated to minigames, connected to the 28th minigame instance on that PaperMC server.  
- 1 minigame PaperMC server *generally* supports 50 minigame instances, each housing 2-4 players.
- Players per minigame is able to dynamically change, and thus change the amount of instances able to be ran on that PaperMC server.

**Notes:**
- Any figure here would most likely change with experimentation of systems.
- Support for dynamically changing if a PaperMC server is a lobby, event, or minigame server might be added.
