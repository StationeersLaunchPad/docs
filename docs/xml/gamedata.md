# GameData Overview

GameData xml files contain configurations for the various systems of the game. You can find the vanilla GameData files in the game install under `rocketstation_Data/StreamingAssets/Data` and `rocketstation_Data/StreamingAssets/Worlds`. These files will always be loaded first, followed by the files in enabled mods.

In a mod, these files can be anywhere inside the `GameData` folder except in a folder named `Language`. The name of the file doesn't matter as long as it has the xml extension. Each file should contain one top-level `GameData` element with any configuration elements inside.

```xml
<?xml version="1.0" encoding="utf-8"?>
<GameData>
  <!-- custom configurations here -->
</GameData>
```

## Recipes
Most devices that consume and produce items (printers, furnaces, centrifuge, etc), follow recipes defined in xml. These recipes can be replaced by mods by defining a recipe for the same item.

Children: [RecipeData](GameData_Elements/recipedata.md)

```xml
<?xml version="1.0" encoding="utf-8"?>
<GameData>
  <CentrifugeRecipes><!-- <RecipeData> --></CentrifugeRecipes>
  <FurnaceRecipes><!-- <RecipeData> --></FurnaceRecipes>
  <AdvancedFurnaceRecipes><!-- <RecipeData> --></AdvancedFurnaceRecipes>
  <ArcFurnaceRecipes><!-- <RecipeData> --></ArcFurnaceRecipes>
  <MicrowaveRecipes><!-- <RecipeData> --></MicrowaveRecipes>
  <PackagingMachineRecipes><!-- <RecipeData> --></PackagingMachineRecipes>
  <AutolatheRecipes><!-- <RecipeData> --></AutolatheRecipes>
  <AutomatedOvenRecipes><!-- <RecipeData> --></AutomatedOvenRecipes>
  <ElectronicsPrinterRecipes><!-- <RecipeData> --></ElectronicsPrinterRecipes>
  <SecurityPrinterRecipes><!-- <RecipeData> --></SecurityPrinterRecipes>
  <RocketManufactoryRecipes><!-- <RecipeData> --></RocketManufactoryRecipes>
  <HydraulicPipeBenderRecipes><!-- <RecipeData> --></HydraulicPipeBenderRecipes>
  <ToolManufactoryRecipes><!-- <RecipeData> --></ToolManufactoryRecipes>
  <ChemistryRecipes><!-- <RecipeData> --></ChemistryRecipes>
  <IngotRecipes><!-- <RecipeData> --></IngotRecipes>
  <RecycleRecipes><!-- <RecipeData> --></RecycleRecipes>
  <TerraformingManufactoryRecipes><!-- <RecipeData> --></TerraformingManufactoryRecipes>
</GameData>
```

## All Elements
??? example "Show"
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <GameData>
      <CentrifugeRecipes><!-- <RecipeData> --></CentrifugeRecipes>
      <FurnaceRecipes><!-- <RecipeData> --></FurnaceRecipes>
      <AdvancedFurnaceRecipes><!-- <RecipeData> --></AdvancedFurnaceRecipes>
      <ArcFurnaceRecipes><!-- <RecipeData> --></ArcFurnaceRecipes>
      <MicrowaveRecipes><!-- <RecipeData> --></MicrowaveRecipes>
      <PackagingMachineRecipes><!-- <RecipeData> --></PackagingMachineRecipes>
      <AutolatheRecipes><!-- <RecipeData> --></AutolatheRecipes>
      <AutomatedOvenRecipes><!-- <RecipeData> --></AutomatedOvenRecipes>
      <ElectronicsPrinterRecipes><!-- <RecipeData> --></ElectronicsPrinterRecipes>
      <SecurityPrinterRecipes><!-- <RecipeData> --></SecurityPrinterRecipes>
      <RocketManufactoryRecipes><!-- <RecipeData> --></RocketManufactoryRecipes>
      <HydraulicPipeBenderRecipes><!-- <RecipeData> --></HydraulicPipeBenderRecipes>
      <ToolManufactoryRecipes><!-- <RecipeData> --></ToolManufactoryRecipes>
      <ChemistryRecipes><!-- <RecipeData> --></ChemistryRecipes>
      <IngotRecipes><!-- <RecipeData> --></IngotRecipes>
      <RecycleRecipes><!-- <RecipeData> --></RecycleRecipes>
      <TerraformingManufactoryRecipes><!-- <RecipeData> --></TerraformingManufactoryRecipes>
      <MinableVisualiser><!-- MinableVisualiserData --></MinableVisualiser>
      <ReagentGrinderRecipes><!-- <ProcessingData> --></ReagentGrinderRecipes>
      <WorldSettings><!-- <World> WorldSettingData --></WorldSettings>
      <Trader><!-- TraderData --></Trader>
      <RoomTypeRule><!-- RoomTypeRuleData --></RoomTypeRule>
      <ContactSlot><!-- ContactSlotData --></ContactSlot>
      <SpaceMap><!-- SpaceMapData --></SpaceMap>
      <CelestialBodies><!-- <CelestialBody> CelestialBodyTemplate --></CelestialBodies>
      <Icon><!-- NodeIcon --></Icon>
      <Spawn><!-- SpawnData --></Spawn>
      <StartCondition><!-- StartConditionData --></StartCondition>
      <StartLocation><!-- StartLocationData --></StartLocation>
      <RandomStartLocation><!-- RoundRobitStartLocationData --></RandomStartLocation>
      <WorldObjective><!-- WorldObjectiveCollection --></WorldObjective>
      <Objective><!-- WorldObjective --></Objective>
      <Buy><!-- BuyData --></Buy>
      <Sell><!-- SellData --></Sell>
      <PaintMixRecipes><!-- <RecipeData> --></PaintMixRecipes>
      <ThingMods><!-- <ThingModData> --></ThingMods>
      <ReagentTradeValues><!-- <ReagentTradeData> --></ReagentTradeValues>
      <GasMoleTradeValues><!-- <GasTradeData> --></GasMoleTradeValues>
      <DifficultySettings><!-- <DifficultySetting> --></DifficultySettings>
      <DefaultRocketNames><!-- <RocketName> --></DefaultRocketNames>
      <GHGIndex><!-- TerraformingGasCurveData --></GHGIndex>
      <AtmosphericScatteringBlend><!-- AtmosphericScatteringBlendData --></AtmosphericScatteringBlend>
      <LifeRequirements><!-- LifeRequirementsData --></LifeRequirements>
      <CustomPlant><!-- CustomPlantData --></CustomPlant>
      <CustomSeed><!-- CustomSeedData --></CustomSeed>
      <Blueprint><!-- BlueprintData --></Blueprint>
      <WeatherEvent><!-- WeatherEvent --></WeatherEvent>
      <ServerProviderData><!-- ServerProvider --></ServerProviderData>
      <Minables><!-- MinablesGenerationData --></Minables>
      <DeepMinables><!-- DeepMinablesGenerationData --></DeepMinables>
      <OreVein><!-- VeinGenerationData --></OreVein>
      <Expression><!-- FacialExpressionData --></Expression>
    </GameData>
    ```