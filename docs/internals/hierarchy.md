# Object Hierarchy

* `Assets.Scripts.Objects.Thing`: Base of all objects in the game
    * `Assets.Scripts.Objects.DynamicThing`: Things that do not have a fixed position
        * `Assets.Scripts.Objects.Item`: DynamicThings that can be stored in an inventory slot
        * `Assets.Scripts.Objects.Entity`: All "living" entities (players, chickens)
    * `Assets.Scripts.Objects.Structure`: Things built by the player at a fixed position
        * `Assets.Scripts.Objects.LargeStructure`: Structures built on the 2m large grid (frames, walls, rocket fuselages)
        * `Assets.Scripts.Objects.SmallGrid`: Structures built on the 0.5m small grid (pipes, cables, devices, etc.)