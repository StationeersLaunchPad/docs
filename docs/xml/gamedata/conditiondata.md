# ConditionData

## BuildStateCondition
```xml
<BuildState
  IsCompleted="boolean"
  CanManufactor="boolean"
  MachineTier="MachineTier"
  BlockGravity="boolean"
/>
```
[+ Base ConditionData](#base-conditiondata)

## ConditionComparable
```xml
<Comparable Compare="CompareOperator"/>
```
[+ Base ConditionData](#base-conditiondata)
??? example "CompareOperator Values"
    - `Less`
    - `EqualOrLess`
    - `Equal`
    - `EqualOrGreater`
    - `Greater`

## DecayCondition
```xml
<Decay Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## DepthCondition
```xml
<Depth Depth="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## DifficultyCondition
```xml
<Difficulty Id="string"/>
```
[+ ConditionComparable](#conditioncomparable)

## EnergyCondition
```xml
<Charge Ratio="number" Percent="number" State="BatteryCellState"/>
```
[+ ConditionComparable](#conditioncomparable)

## GasCondition
```xml
<Gas
  Type="GasType"
  Percent="number"
  Moles="number"
  PartialPressure="number"
/>
```
[+ ConditionComparable](#conditioncomparable)

## GrowthStateCondition
```xml
<GrowthState Value="number" IsPlanted="bool"/>
```
[+ ConditionComparable](#conditioncomparable)

## LogicCondition
```xml
<LogicType Type="LogicType" Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## MoleCondition
```xml
<Moles Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## PercentCondition
```xml
<Percent Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## PlantRecordCondition
```xml
<PlantRecord Status="PlantStatusType" Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## PressureCondition
```xml
<Pressure kPa="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## QuantityCondition
```xml
<Quantity Value="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## ReagentCondition
```xml
<Reagents Total="number" _Reagent_="number" />
```
[+ ConditionComparable](#conditioncomparable)

## SizeCondition
```xml
<Size X="number" Y="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## SurvivalPropertyCondition
```xml
<SurvivalProperty
  Type="EntitySurvivalProperty"
  Percent="number"
  Ratio="number"
/>
```
[+ ConditionComparable](#conditioncomparable)

## TemperatureComparableCondition
```xml
<Temperature Celsius="number" Kelvin="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## ThingCountCondition
```xml
<ThingCount Id="string" Count="number"/>
```
[+ ConditionComparable](#conditioncomparable)

## CursorThingCondition
```xml
<CursorThing Id="string"/>
```
[+ Base ConditionData](#base-conditiondata)

## CustomNameCondition
```xml
<CustomName Value="string"/>
```
[+ Base ConditionData](#base-conditiondata)

## EntityStateCondition
```xml
<EntityState>
  <IsOnline Value="bool"/>
  <State Value="EntityState"/>
</EntityState>
```
[+ Base ConditionData](#base-conditiondata)

## InCellCondition
```xml
<InCell X="number" Y="number" Z="number"/>
```
[+ Base ConditionData](#base-conditiondata)

## InteractableCondition
```xml
<Interactable Action="InteractableType" State="number"/>
```
[+ Base ConditionData](#base-conditiondata)

## NetworkCondition
```xml
<Network Type="StructureNetworkType"/>
```
[+ Base ConditionData](#base-conditiondata)

## ObjectiveCompleteCondition
```xml
<ObjectiveComplete Id="string"/>
```
[+ Base ConditionData](#base-conditiondata)

## PlantStatusCondition
```xml
<PlantStatus Status="PlantStatusType" Value="boolean"/>
```
[+ Base ConditionData](#base-conditiondata)

## PreSpawnedCondition
```xml
<PreSpawned Value="boolean"/>
```
[+ Base ConditionData](#base-conditiondata)

## RegionCondition
```xml
<Region Id="string"/>
```
[+ Base ConditionData](#base-conditiondata)

## RoomCondition
```xml
<Room RoomType="RoomType" MinSize="number" MaxSize="number"/>
```
[+ Base ConditionData](#base-conditiondata)

## SpeciesCondition
```xml
<Species Id="SpeciesClass"/>
```
[+ Base ConditionData](#base-conditiondata)

## SurfaceCondition
```xml
<Surface Value="boolean"/>
```
[+ Base ConditionData](#base-conditiondata)

## TemperatureRangeCondition
```xml
<TemperatureRange Unit="TemperatureType" Min="number" Max="number"/>
```
[+ Base ConditionData](#base-conditiondata)

## ThingPrefabCondition
```xml
<Prefab Id="string"/>
```
[+ Base ConditionData](#base-conditiondata)

## ChildItemPrefabCondition
```xml
<Item Id="string" SlotId="string" SlotIndex="number"/>
```
[+ Base ConditionData](#base-conditiondata)

## TraderContactCondition
```xml
<Contact IsResolved="boolean" IsContacted="boolean" IsLanded="boolean"/>
```
[+ Base ConditionData](#base-conditiondata)

## Base ConditionData
??? example "XML Structure"
    ```xml
    <Condition Hidden="boolean">
      <Conditions><!-- ConditionDataCollection --></Conditions>
      <Room /> <!-- RoomCondition -->
      <Network /> <!-- NetworkCondition -->
      <SurvivalProperty /> <!-- SurvivalPropertyCondition -->
      <CustomName /> <!-- CustomNameCondition -->
      <Prefab /> <!-- ThingPrefabCondition -->
      <Contact /> <!-- TraderContactCondition -->
      <Size /> <!-- SizeCondition -->
      <Temperature /> <!-- TemperatureComparableCondition -->
      <GrowthState /> <!-- GrowthStateCondition -->
      <PlantStatus /> <!-- PlantStatusCondition -->
      <PlantRecord /> <!-- PlantRecordCondition -->
      <LogicType /> <!-- LogicCondition -->
      <Reagents /> <!-- ReagentCondition -->
      <BuildState /> <!-- BuildStateCondition -->
      <Interactable /> <!-- InteractableCondition -->
      <Quantity /> <!-- QuantityCondition -->
      <Decay /> <!-- DecayCondition -->
      <Gas /> <!-- GasCondition -->
      <Pressure /> <!-- PressureCondition -->
      <TemperatureRange /> <!-- TemperatureRangeCondition -->
      <Percent /> <!-- PercentCondition -->
      <Item /> <!-- ChildItemPrefabCondition -->
      <Moles /> <!-- MoleCondition -->
      <Charge /> <!-- EnergyCondition -->
      <Difficulty /> <!-- DifficultyCondition -->
      <Species /> <!-- SpeciesCondition -->
      <PreSpawned /> <!-- PreSpawnedCondition -->
      <InCell /> <!-- InCellCondition -->
      <Region /> <!-- RegionCondition -->
      <Surface /> <!-- SurfaceCondition -->
      <Depth /> <!-- DepthCondition -->
    </Condition>
    ```

## ConditionDataCollection
??? example "XML Structure"
    ```xml
    <Conditions Hidden="boolean" Operator="LogicOperator">
      <Conditions><!-- ConditionDataCollection -->
      <Room /> <!-- RoomCondition -->
      <CustomName /> <!-- CustomNameCondition -->
      <Prefab /> <!-- ThingPrefabCondition -->
      <Contact /> <!-- TraderContactCondition -->
      <Size /> <!-- SizeCondition -->
      <Temperature /> <!-- TemperatureComparableCondition -->
      <GrowthState /> <!-- GrowthStateCondition -->
      <PlantStatus /> <!-- PlantStatusCondition -->
      <PlantRecord /> <!-- PlantRecordCondition -->
      <LogicType /> <!-- LogicCondition -->
      <Reagents /> <!-- ReagentCondition -->
      <BuildState /> <!-- BuildStateCondition -->
      <Interactable /> <!-- InteractableCondition -->
      <Decay /> <!-- DecayCondition -->
      <Quantity /> <!-- QuantityCondition -->
      <Gas /> <!-- GasCondition -->
      <Pressure /> <!-- PressureCondition -->
      <TemperatureRange /> <!-- TemperatureRangeCondition -->
      <Item /> <!-- ChildItemPrefabCondition -->
      <Percent /> <!-- PercentCondition -->
      <Moles /> <!-- MoleCondition -->
      <Charge /> <!-- EnergyCondition -->
      <Difficulty /> <!-- DifficultyCondition -->
      <Species /> <!-- SpeciesCondition -->
      <PreSpawned /> <!-- PreSpawnedCondition -->
      <InCell /> <!-- InCellCondition -->
      <Region /> <!-- RegionCondition -->
      <Surface /> <!-- SurfaceCondition -->
      <Depth /> <!-- DepthCondition -->
    </Conditions>
    ```
??? example "LogicOperator Values"
    - `All`
    - `Any`
    - `None`