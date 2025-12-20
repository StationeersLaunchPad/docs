# RecipeData
`<RecipeData>` elements define the recipe used to create an item, or for Centrifuge and Recyler what to produce when destroying an item.

??? example "Structure"
    ```xml
    <RecipeData>
      <PrefabName>ItemGasCanisterEmpty</PrefabName>
      <RecipeTier>TierOne</RecipeTier>
      <Output>1</Output>
      <Recipe>
        <!-- reagents -->
        <Time>10</Time>
        <Energy>500</Energy>
        <Temperature>
          <Start>1000</Start>
          <Stop>2000</Start>
        </Temperature>
        <Pressure>
          <Start>1000</Start>
          <Stop>10000</Stop>
        </Pressure>
        <RequiredMix>
          <!-- gasses -->
          <Rule>Pure</Rule>
        </RequiredMix>
      </Recipe>
    </RecipeData>
    ```

## Examples

=== "Printer"
    ```xml
    <RecipeData>
      <PrefabName>ItemKitAutolathe</PrefabName>
      <Recipe>
        <Iron>20</Iron>
        <Copper>10</Copper>
        <Gold>2</Gold>
        <Time>180</Time>
        <Energy>36000</Energy>
      </Recipe>
    </RecipeData>
    ```

=== "Furnace"
    ```xml
    <RecipeData>
      <PrefabName>ItemWaspaloyIngot</PrefabName>
      <Recipe>
        <Lead>.5</Lead>
        <Nickel>.25</Nickel>		
        <Silver>.25</Silver>
        <Temperature>
          <Start>400</Start>
          <Stop>800</Stop>
        </Temperature>
        <Pressure>
          <Start>50000</Start>
          <Stop>99999</Stop>
        </Pressure>
      </Recipe>
      <Output>0.25</Output>
    </RecipeData>
    ```

=== "Arc Furnace"
    ```xml
    <RecipeData>
      <PrefabName>ItemGoldIngot</PrefabName>
      <Recipe>
        <Gold>1</Gold>
        <Time>6</Time>
        <Energy>2000</Energy>
      </Recipe>
    </RecipeData>
    ```

=== "Centrifuge"
    ```xml
    <RecipeData>
      <PrefabName>ItemBiomass</PrefabName>
      <Recipe>
        <Biomass>1</Biomass>
      </Recipe>
    </RecipeData>
    ```

=== "Ingot"
    Ingot recipes are used to produce ingots when emptying a printer. They should only contain a single reagent
    ```xml
    <RecipeData>
      <PrefabName>ItemIronIngot</PrefabName>
      <Recipe>
        <Iron>1</Iron>
      </Recipe>
    </RecipeData>
    ```

## Child Elements

`<PrefabName>` (required)

:   Which item to produce or consume for this recipe. This matches the `Thing.PrefabName` field, or the `Prefab Name` in Stationpedia.

`<RecipeTier>` (optional)

:   The minimum machine tier needed for this recipe. Only used for printers.

    Possible Values

    - `Undefined` (default): Any tier
    - `TierOne`: Basic tier. Effectively the same as `Undefined`
    - `TierTwo`: Upgraded tier. Requires `Printer Mod` applied to a basic printer
    - `TierThree`: Unused. Will not allow the recipe to be printed by any vanilla printer

`<Output>` (optional)

:   The multiplier applied to the output amount, default 1. Only used for furnaces. The final result amount is the sum of the reagents multiplied by the `Output` value. This is set to 0.25 for the vanilla superalloys.

`<Recipe>` (required)

:   What reagents to consume or produce for the recipe.

    ??? example "Reagents"
        Any reagent not needed for the recipe can be omitted
        ```xml
        <Recipe>
          <Flour>1</Flour>
          <Milk>1</Milk>
          <Egg>1</Egg>
          <Iron>1</Iron>
          <Gold>1</Gold>
          <Carbon>1</Carbon>
          <Uranium>1</Uranium>
          <Copper>1</Copper>
          <Steel>1</Steel>
          <Hydrocarbon>1</Hydrocarbon>
          <Silver>1</Silver>
          <Nickel>1</Nickel>
          <Lead>1</Lead>
          <Electrum>1</Electrum>
          <Invar>1</Invar>
          <Constantan>1</Constantan>
          <Solder>1</Solder>
          <Plastic>1</Plastic>
          <Silicon>1</Silicon>
          <SalicylicAcid>1</SalicylicAcid>
          <Alcohol>1</Alcohol>
          <Oil>1</Oil>
          <Potato>1</Potato>
          <Tomato>1</Tomato>
          <Fenoxitone>1</Fenoxitone>
          <ColorRed>1</ColorRed>
          <ColorGreen>1</ColorGreen>
          <ColorBlue>1</ColorBlue>
          <ColorYellow>1</ColorYellow>
          <ColorOrange>1</ColorOrange>
          <Pumpkin>1</Pumpkin>
          <Rice>1</Rice>
          <Waspaloy>1</Waspaloy>
          <Stellite>1</Stellite>
          <Inconel>1</Inconel>
          <Hastelloy>1</Hastelloy>
          <Astroloy>1</Astroloy>
          <Cobalt>1</Cobalt>
          <Corn>1</Corn>
          <Wheat>1</Wheat>
          <Biomass>1</Biomass>
          <Soy>1</Soy>
          <Mushroom>1</Mushroom>
          <Sugar>1</Sugar>
          <Cocoa>1</Cocoa>
          <Cheese>1</Cheese>
        </Recipe>
        ```

    `<Time>`

    :   How long in seconds the recipe takes. Used for printers, arc furnace, chemistry station, microwave, packaging machine.

    `<Energy>`

    :   How much energy in Joules is needed for this recipe. Used for printers, arc furnace, furnaces.

        For printers, this defines the total energy needed for the recipe in addition to the base energy requirement of the printer. This energy consumption will be spread out over the duration of the print.

        For arc furnaces, this defines the energy needed every tick in order to continue processing.

        For furnaces, this defines the energy removed from the furnace atmosphere per unit of produced ingot.

    `<Temperature>`

    :   The range of temperatures in Kelvin that can produce this recipe. Used for furnace and arc furnace.

        For arc furnace recipes, this range must contain `5273.15` for the recipe to be valid.

    `<Pressure>`

    :   The range of pressures in kPa that can produce this recipe. Used for furnace and and arc furnace.

        For arc furnace recipes, this range must contain `101.325` for the recipe to be valid.

    `<RequiredMix>`

    :   The required number of moles of each gas to be consumed per unit of this recipe. Used for furnace only.

        The `Rule` child element defines the requirements of a valid gas mixture.

        - `None` (default) requires that each gas has at least the specified number of moles
        - `Pure` requires that non-zero gas requirements have at least the specified number of moles, and that zero gas requirements have no moles present.

        ??? example "Gasses"
            Any gas not needed for the recipe can be omitted
            ```xml
            <RequiredMix>
              <Oxygen>1</Oxygen>
              <Nitrogen>1</Nitrogen>
              <CarbonDioxide>1</CarbonDioxide>
              <Volatiles>1</Volatiles>
              <Pollutant>1</Pollutant>
              <Water>1</Water>
              <PollutedWater>1</PollutedWater>
              <NitrousOxide>1</NitrousOxide>
              <LiquidNitrogen>1</LiquidNitrogen>
              <LiquidOxygen>1</LiquidOxygen>
              <LiquidVolatiles>1</LiquidVolatiles>
              <Steam>1</Steam>
              <LiquidCarbonDioxide>1</LiquidCarbonDioxide>
              <LiquidPollutant>1</LiquidPollutant>
              <LiquidNitrousOxide>1</LiquidNitrousOxide>
              <Hydrogen>1</Hydrogen>
              <LiquidHydrogen>1</LiquidHydrogen>
            </RequiredMix>
            ```

## Parent Elements
`RecipeData` elements are children of most top-level `Recipes` elements.
??? example "Full Parent List"
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