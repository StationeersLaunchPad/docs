# SpawnData
`<Spawn>` elements define a set of spawn actions for creating a set of starting equipment or items, as well as creating prebuilt structures and room atmospheres for tutorials.

??? example "XML Structure"
    ```xml
    <Spawn
        Id="string"
        Event="string"
        HideInStartScreen="boolean"
        ShowInSpawnMenu="boolean"
        StartScreenHeader="string">
      <Name Key="string" />
      <Species><!-- SpeciesCondition --></Species>
      <Difficulty><!-- DifficultyCondition --></Difficulty>
      <SurvivalProperty><!-- SurvivalPropertyAction --></SurvivalProperty>
      <Item><!-- DynamicSpawnData --></Item>
      <DynamicThing><!-- DynamicSpawnData --></DynamicThing>
      <Structure><!-- StructureSpawnData --></Structure>
      <WorldAtmosphere><!-- WorldAtmosphereSpawnData --></WorldAtmosphere>
      <Spawn><!-- SpawnData --></Spawn>
    </Spawn>
    ```

### Examples

=== "Crate"
    ```xml title="Spawn a green crate with basic hydroponics setup"
    <Spawn Id="PotatoSupplies">
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
    </Spawn>
    ```

=== "Equipment"
    ```xml title="Spawn emergency equipment in the proper slots"
    <Spawn Id="EmergencyRespawnHuman">
      <Item Id="ItemEmergencySpaceHelmet" SlotId="Helmet"/>
      <Item Id="ItemEmergencyEvaSuit" SlotId="Suit">
        <Item Id="ItemGasCanisterEmpty" SlotId="AirTank">
          <Name Key="SpawnDataOxygenCanister"/>
          <Color Id="White"/>
          <Gas Type="Oxygen" Moles="150" Celsius="20"/>
        </Item>
        <Item Id="ItemGasFilterCarbonDioxide" SlotId="Filter"/>
        <Item Id="ItemGasCanisterEmpty" SlotId="WasteTank"/>
        <Item Id="ItemBatteryCell" SlotId="LifeSupport">
          <Charge State="Full"/>
        </Item>
      </Item>
      <Spawn Id="EmergencyToolbelt"/>
    </Spawn>
    ```

=== "Conditional"
    ```xml title="Spawn EmergencyRespawnHuman defined elsewhere when playing as Human on Stationeer difficulty"
    <Spawn Id="EmergencyRespawnHuman" Event="RespawnPlayerKit">
      <Species Id="Human"/>
      <Difficulty Id="Stationeer" Compare="Equal"/>
    </Spawn>
    ```

### Valid Check

In order to be considered valid, a `SpawnData` must have at least one of the following children:

- `<Item>`
- `<DynamicThing>`
- `<Spawn>`
- `<Structure>`
- `<WorldAtmosphere>`

When not valid, this is instead a reference spawn and the `Id` attribute is used to look up `SpawnData` defined elsewhere to execute. Reference spawns can still specify all attributes to configure its display in the New World menu and which `Event` it executes on, as well as `<Species>` and `<Difficulty>` conditions to further filter its execution.

### Attributes

#### `Id`
:   When valid, registers this `SpawnData` globally for others to reference. Otherwise, specifies what `SpawnData` to lookup and execute here.

#### `Event`
:   When this `SpawnData` is a top-level child of a `StartConditionData` or `WorldSettingData`, specifies when this spawn should be executed. Otherwise this attribute is ignored.

    Possible Values

    - `None` (default): Don't execute automatically
    - `NewWorld`: Executed once when creating a new world
    - `NewPlayerKit`: Executed once for each player to create their equipment when first joining the world
    - `RespawnPlayerKit`: Executed once for each player to create their equipment when respawning
    - `NewPlayer`: Executed once for each player when first joining the world. Spawns items loose in the world near the player
    - `RespawnPlayer`: Executed once for each player when respawning. Spawns items loose in the world near the player

#### `HideInStartScreen`
:   When `true`, this `SpawnData` will not be displayed in the starting items on the New World menu

#### `ShowInSpawnMenu`
:   When `true`, this `SpawnData` will be available in the creative spawn menu

#### `StartScreenHeader`
:   The localization key of the subtitle text for this spawn in the New World menu

### Child Elements

#### Name
`<Name Key="string" Value="string" />` `LocalizedStringReference`
:   Name of this `SpawnData`. Currently only used as the display name in the creative spawn menu. May be specified by a localization `Key` or a fixed `Value`

#### Conditions
`<Species>` `SpeciesCondition`
`<Difficulty>` `DifficultyCondition`
:   Condition elements that restrict when this spawn will occur. See [ConditionData (TODO)](#)

#### Survival Property
[`<SurvivalProperty>` `SurvivalPropertyAction`](actiondata.md#survivalpropertyaction)
:   Sets a survival property (hydration, mood, etc) of the player or spawned entity

#### Item Spawn
[`<Item>` `DynamicSpawnData`](thingspawndata.md#dynamicspawndata)
[`<DynamicThing>` `DynamicSpawnData`](thingspawndata.md#dynamicspawndata)
:   Items to spawn as part of this `SpawnData`

#### Structure Spawn
[`<Structure>` `StructureSpawnData`](thingspawndata.md#structurespawndata)
:   Structures to spawn as part of this `SpawnData`. Primarily used for prebuilt structures in tutorials

#### Atmosphere
`<WorldAtmosphere>` `WorldAtmosphereSpawnData`
:   Atmospheres to spawn as part of this `SpawnData`. Primarily used to fill rooms with specific gasses in tutorials

    ??? example "Structure"
        ```xml
        <WorldAtmosphere X="100" Y="200" Z="300" RoomId="1234>
          <Gas Type="Oxygen" Moles="100" Celsius="20" />
        </WorldAtmosphere>
        ```
    
    `X`/`Y`/`Z`
    :   World grid coordinates of the atmosphere

    `RoomId`
    :   Id of prebuilt `Room` this atmosphere is a member of

    [`<Gas>` `GasAction`](actiondata.md#gasaction) (repeated)
    :   A gas to spawn in this atmosphere

#### Child Spawns
`<Spawn>` `SpawnData`

:   Child spawn elements to be executed as part of this `SpawnData`. These can be fully defined spawns that will be registered globally by their `Id` (if present), or references to spawns defined elsewhere.

### Parent Elements

=== "Top-Level Definition"
    ```xml title="Define a spawn to be referenced by Id"
    <GameData>
      <Spawn></Spawn>
    </GameData>
    ```

=== "World Spawn"
    ```xml title="Define a spawn to execute on a specific Event"
    <GameData>
      <StartCondition>
        <Spawn></Spawn>
      </StartCondition>
      <WorldSettings>
        <World>
          <Spawn></Spawn>
        </World>
      </WorldSettings>
    </GameData>
    ```

=== "Nested Spawn"
    ```xml title="Run another spawn (referenced by Id and/or with conditions)"
    <Spawn>
      <Spawn></Spawn>
    <Spawn>
    ```
    ```xml title="Run a spawn as a child of an item to fill slots"
    <DynamicThing>
      <Spawn></Spawn>
    </DynamicThing>
    ```
    ```xml title="Run a spawn as a child of a structure to fill slots"
    <Structure>
      <Spawn></Spawn>
    </Structure>
    ```