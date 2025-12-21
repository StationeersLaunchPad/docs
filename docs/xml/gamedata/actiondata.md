# ActionData

## BuildStateAction
```xml
<BuildState Index="number"/>
```

## ChargeAction
```xml
<Charge State="BatteryCellState"/>
```

## GasAction
```xml
<Gas
  Type="GasType"
  Moles="number"
  Litres="number"
  Celsius="number"
  Kelvin="number"
  Energy="number"
/>
```
??? example "GasType Values"
      - Oxygen
      - Nitrogen
      - CarbonDioxide
      - Volatiles
      - Pollutant
      - Water
      - NitrousOxide
      - LiquidNitrogen
      - LiquidOxygen
      - LiquidVolatiles
      - Steam
      - LiquidCarbonDioxide
      - LiquidPollutant
      - LiquidNitrousOxide
      - Hydrogen
      - LiquidHydrogen
      - PollutedWater

## GeneAction
```xml
<Gene Id="Gene" Value="number"/>
```
??? example "Gene Values"
    - GrowthTimeMultiplier
    - DarkPerDay
    - LightPerDay
    - DroughtTolerance
    - WaterUsage
    - LowPressureResistance
    - LowTemperatureResistance
    - UndesiredGasTolerance
    - GasProduction
    - HighPressureResistance
    - HighTemperatureResistance
    - SuffocationTolerance
    - LowPressureTolerance
    - LowTemperatureTolerance
    - HighPressureTolerance
    - HighTemperatureTolerance
    - UndesiredGasResistance
    - LightTolerance
    - DarknessTolerance

## InteractionAction
```xml
<Interaction Type="InteractableType" Value="number">
  <Delay Seconds="number" Minutes="number" Hours="number" Days="number"/>
</Interaction>
```

## LogicValueAction
```xml
<Logic Type="LogicType" Value="number"/>
```

## MovePlayerAction
```xml
<MovePlayer SlotId="string" SlotIndex="number"/>
```

## PercentAction
```xml
<Percent Value="number"/>
```

## PopupAction / CompletedTutorialPopupAction
```xml
<Popup Delay="number">
  <Title Key="string"/>
  <Text Key="string"/>
</Popup>
<CompletedTutorialPopup Delay="number">
  <Title Key="string"/>
  <Text Key="string"/>
</CompletedTutorialPopup>
```

## QuantityAction
```xml
<Quantity Value="number"/>
```

## ReagentAction
```xml
<Reagents _Reagent_="number"/>
```

## SourceCodeAction
```xml
<SourceCode>
  <Text>string</Text>
</SourceCode>
```

## SurvivalPropertyAction
```xml
<SurvivalProperty type="EntitySurvivalProperty" Percent="number"/>
```
??? example "EntitySurvivalProperty Values"
    - OxygenQuality
    - Nutrition
    - Hydration
    - Mood
    - Hygiene
    - FoodQuality
    - Health
