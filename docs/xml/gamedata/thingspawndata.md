
# ThingSpawnData
ThingSpawnData elements define items and structures to spawn into the world

## `DynamicSpawnData`
`<DynamicThing>` and `<Item>` elements (interchangeable) are used to create items (loose objects that can be dropped on the ground or put in inventories).

??? example "XML Structure"
    Includes all [`ThingSpawnData` Attributes](#thingspawndata-attributes) and [`ThingSpawnData` Child Elements](#thingspawndata-children) in addition to:
    ```xml
    <Item
        SlotIndex="integer"
        SlotId="string"
        SlotClass="Slot.Class"
        ...ThingSpawnData Attributes>
      <!-- ThingSpawnData Child Elements -->
    </Item>
    ```

### Examples

=== "Simple Item"
    ```xml title="Single Potato Seedbag"
    <Item Id="SeedBag_Potato"/>
    ```

=== "Crate"
    ```xml title="Green crate with supplies to grow potatoes"
    <DynamicThing Id="DynamicCrate">
      <Color Id="Green"/>
      <Item Id="SeedBag_Potato">
        <Quantity Value="3"/>
      </Item>
      <Item Id="ItemHydroponicTray">
        <Quantity Value="5"/>
      </Item>
      <Item Id="ItemKitPipeUtilityLiquid">
        <Quantity Value="1"/>
      </Item>
      <Item Id="ItemKitPipeLiquid">
        <Quantity Value="20"/>
      </Item>
    </DynamicThing>
    ```

### Attributes
Includes all [`ThingSpawnData` Attributes](#thingspawndata-attributes)

Uses the first found slot attribute (in order `SlotIndex`, `SlotId`, `SlotClass`) to determine which slot in the parent to spawn this item into. If the first slot attribute does not match any available parent slots, the item will be spawned loose in the world. If no slot attributes are specified, the item will be placed in the first compatible slot, or loose in the world if no slots are available.

#### `SlotIndex`
:   Numeric index (starting from 0) of the slot to spawn this item into

#### `SlotId`
:   The ID of a specific slot. Primarily for slots that serve a specific function in the parent
    ??? example "Common SlotIds"
        - `Helmet`
        - `Suit`
        - `Back`
        - `Belt`
        - `Uniform`
        - `AirTank`
        - `WasteTank`
        - `LifeSupport`
        - `Propellant`
        - `Filter`
        - `Tool`
        - `Battery`
        - `GasCanister`
        - `Ore`
        - `Input`
        - `Import`
        - `Import2`
        - `Export`
        - `Export2`

#### `SlotClass`
:   The type of item the slot is restricted to
    ??? example "Slot Classes"
        - `None`
        - `Helmet`
        - `Suit`
        - `Back`
        - `GasFilter`
        - `GasCanister`
        - `Motherboard`
        - `Circuitboard`
        - `DataDisk`
        - `Organ`
        - `Ore`
        - `Plant`
        - `Uniform`
        - `Entity`
        - `Battery`
        - `Egg`
        - `Belt`
        - `Tool`
        - `Appliance`
        - `Ingot`
        - `Torpedo`
        - `Cartridge`
        - `AccessCard`
        - `Magazine`
        - `Circuit`
        - `Bottle`
        - `ProgrammableChip`
        - `Glasses`
        - `CreditCard`
        - `DirtCanister`
        - `SensorProcessingUnit`
        - `LiquidCanister`
        - `LiquidBottle`
        - `Wreckage`
        - `SoundCartridge`
        - `DrillHead`
        - `ScanningHead`
        - `Flare`
        - `Blocked`
        - `SuitMod`
        - `Crate`
        - `Portables`
        - `RocketPayload`

### Child Elements
Includes all [`ThingSpawnData` Child Elements](#thingspawndata-children)

### Parent Elements

=== "Top-Level Item"
    ```xml title="Create an item in world, or equipped to the player"
    <Spawn>
      <Item></Item>
    </Spawn>
    ```

=== "Child Item"
    ```xml title="Create an item in a container item"
    <Item>
      <Item></Item>
    </Item>
    ```
    ```xml title="Create an item slotted in a structure"
    <Structure>
      <Item></Item>
    </Structure>
    ```

## `StructureSpawnData`
`<Structure>` elements are used to create pre-built structures in the world. Structures created this way are not subject to placement restrictions, so care must be taken to avoid creating invalid structures.

??? example "XML Structure"
    Includes all [`ThingSpawnData` Attributes](#thingspawndata-attributes) and [`ThingSpawnData` Child Elements](#thingspawndata-children)
    ```xml
    <Structure
        ...ThingSpawnData Attributes>
      <!-- ThingSpawnData Child Elements -->
    </Structure>
    ```

### Examples

=== "Simple Structure"
    ```xml title="Completed Iron Frame"
    <Structure Id="StructureFrameIron">
      <SpawnPosition Rule="Explicit">
        <Offset x="-145" y="39" z="-7" />
      </SpawnPosition>
      <BuildState Index="2" />
    </Structure>
    ```

=== "Structure with Children"
    ```xml title="Locker with tools"
    <Structure Id="StructureLockerSmall">
      <Color Id="ColorYellow" />
      <SpawnPosition Rule="Explicit">
        <Offset x="-138.5" y="44" z="-9" />
        <Rotation x="0" y="270" z="0" />
      </SpawnPosition>
      <Interaction Type="Open" Value="1" />
      <Item Id="ItemWrench" SlotIndex="0" />
      <Item Id="ItemCrowbar" SlotIndex="1" />
      <Item Id="ItemDrill" SlotIndex="2">
        <Item Id="ItemBatteryCellLarge">
          <Charge State="Full" />
        </Item>
      </Item>
    </Structure>
    ```

### Attributes
Includes all [`ThingSpawnData` Attributes](#thingspawndata-attributes)

### Child Elements
Includes all [`ThingSpawnData` Child Elements](#thingspawndata-children)

### Parent Elements

```xml title="Top-Level Structure Spawn"
<Spawn>
  <Structure></Structure>
</Spawn>
```

## `ThingSpawnData`
`ThingSpawnData` is not used directly as an xml element, but is the base for both `DynamicSpawnData` and `StructureSpawnData`. All attributes and child elements here can be used on both.

??? example "XML Structure"
    ```xml
    <Thing
        Id="string"
        HideInStartScreen="boolean"
        ExpandInStartScreen="boolean"
        ShowDeepStartScreenTooltip="boolean"
        SlotIndex="integer"
        SlotId="string"
        SlotClass="Slot.Class">
      <Name Key="string">
      <Color Id="string" />
      <SpawnPosition Rule="SpawnPositionRule">
        <Offset x="number" y="number" z="number" />
        <Rotation x="number" y="number" z="number" />
      </SpawnPosition>
      <Species><!-- SpeciesCondition --></Species>
      <Difficulty><!-- DifficultyCondition --></Difficulty>
      <Logic><!-- LogicValueAction --></Logic>
      <BuildState><!-- BuildStateAction --></BuildState>
      <Interaction><!-- InteractionAction --></Interaction>
      <MovePlayer><!-- MovePlayerAction --></MovePlayer>
      <Gene><!-- GeneAction --></Gene>
      <Quantity><!-- QuantityAction --></Quantity>
      <Percent><!-- PercentAction --></Percent>
      <Reagents><!-- ReagentAction --></Reagents>
      <Charge><!-- ChargeAction --></Charge>
      <Gas><!-- GasAction --></Gas>
      <SourceCode><!-- SourceCodeAction --></SourceCode>
      <Item><!-- DynamicSpawnData --></Item>
      <DynamicThing><!-- DynamicSpawnData --></DynamicThing>
      <Spawn><!-- SpawnData --></Spawn>
    </Thing>
    ```

### Attributes { #thingspawndata-attributes }

#### `Id` (required)
:   Which prefab to spawn. This matches the `Thing.PrefabName` field, or the `Prefab Name` in Stationpedia.

#### `HideInStartScreen`
:   If `true`, this item will not be listed on the New World menu as part of the starting items

#### `ExpandInStartScreen`
:   If `true`, this item will have its children expanded in the New World menu

#### `ShowDeepStartScreenTooltip`
:   If `true`, hovering over this item in the New World menu will display a tooltip with all nested children

### Child Elements { #thingspawndata-children }

#### Custom Name
`<Name Key="string" Value="string">` `LocalizedStringReference`
:   Custom name of the spawned thing. Can be specified by localization `Key` or a fixed `Value`

#### Custom Color
`<Color Id="string" />` `ColorSwatchReference`
:   Custom color of the spawned thing
    
    Possible Values:

    - `Blue` / `ColorBlue`
    - `Gray` / `ColorGray`
    - `Green` / `ColorGreen`
    - `Orange` / `ColorOrange`
    - `Red` / `ColorRed`
    - `Yellow` / `ColorYellow`
    - `White` / `ColorWhite`
    - `Black` / `ColorBlack`
    - `Brown` / `ColorBrown`
    - `Khaki` / `ColorKhaki`
    - `Pink` / `ColorPink`
    - `Purple` / `ColorPurple`

#### Spawn Position
`<SpawnPosition>` `SpawnPositionData`
:   Where the thing should be spawned. When this element is not specified, the position defaults to the `Random` `Rule`

    ??? example "XML Structure"
        ```xml
        <SpawnPosition Rule="SpawnPositionRule">
          <Offset x="number" y="number" z="number />
          <Rotation x="number" y="number" z="number" />
        </SpawnPosition>
        ```
    
    `Rule`
    :   Specifies how to interpret the SpawnPosition data to select the world position 

        Possible Values:

        - `None` (default): at the player spawn location
        - `Random`: random location inside the `SpawnRadius` of the player start location
        - `Radius`: random location at `SpawnRadius` distance from the player start location
        - `Explicit`: at world coordinates specified by `Offset`
    
    `Offset`
    :   If `Rule` is `Explicit`, the world coordinates to spawn at

    `Rotation`
    :   If `Rule` is `None` or `Explicit`, the rotation in degrees of the spawned thing

#### Conditions
`<Species>` `SpeciesCondition`
`<Difficulty>` `DifficultyCondition`
:   Conditions that must match for this thing to be spawned. See [ConditionData (TODO)](#)

    !!! note
        Currently the `<Species>` condition can never match as the player is not used as the target to match against.

#### Actions
[`<Logic>` `LogicValueAction`](actiondata.md#logicvalueaction)
[`<BuildState>` `BuildStateAction`](actiondata.md#buildstateaction)
[`<Interaction>` `InteractionAction`](actiondata.md#interactionaction)
[`<MovePlayer>` `MovePlayerAction`](actiondata.md#moveplayeraction)
[`<Gene>` `GeneAction`](actiondata.md#geneaction)
[`<Quantity>` `QuantityAction`](actiondata.md#quantityaction)
[`<Percent>` `PercentAction`](actiondata.md#percentaction)
[`<Reagents>` `ReagentAction`](actiondata.md#reagentaction)
[`<Charge>` `ChargeAction`](actiondata.md#chargeaction)
[`<Gas>` `GasAction`](actiondata.md#gasaction)
[`<SourceCode>` `SourceCodeAction`](actiondata.md#sourcecodeaction)
:   Actions to apply to the created thing.

#### Child Items
[`<Item>` `DynamicSpawnData`](#dynamicspawndata)
[`<DynamicThing>` `DynamicSpawnData`](#dynamicspawndata)
:   Child items to create in slots of the current created thing. If no slots are available, these will be spawned loose in the world.

#### Child Spawns
[`<Spawn>` `SpawnData`](spawndata.md)
:   Child `SpawnData` elements to spawn in slots of this thing. This allows you to use reference spawns to re-use child item spawn definitions.
