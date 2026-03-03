# Mod Structure

Mods can be developed locally by adding a folder to `%home%/Documents/my games/Stationeers/mods/` with files for the mod.

## Layout
```
About/
  About.xml # This file is required for the game to recognize this as a mod
  Preview.png # Image shown in the in-game workshop menu
  thumb.png # Thumbnail image in steam workshop (must be <1MB)
GameData/
  *.xml # game data xml files (recipes, traders, start conditions, etc.)
  Language/
    *.xml # localization xml files
```

## About.xml format
### Builtin
The game supports a small set of builtin fields:
```xml
<?xml version="1.0" encoding="utf-8"?>
<ModMetadata>
  <!-- Title in workshop and display name in-game -->
  <Name>My Mod</Name>
  <!-- Author and Version are for in-game display only -->
  <Author>Me</Author>
  <Version>1.2.3</Version>
  <!-- Description is shown in the workshop and in-game -->
  <Description>
    [h1]My Mod[/h1]
  </Description>
  <!-- Steam workshop ID. Will be automatically added to xml file after upload -->
  <WorkshopHandle>12345678</WorkshopHandle>
  <!-- Custom tags for workshop. The Mod tag will automatically be added -->
  <Tags>
    <Tag>Special</Tag>
  </Tags>
</ModMetadata>
```
Use [steam text formatting](https://steamcommunity.com/comment/Recommendation/formattinghelp) in the `Description` field so it is formatted properly for the workshop.

### StationeersLaunchPad
When using [StationeersLaunchPad](https://github.com/StationeersLaunchPad/StationeersLaunchPad), an additional set of fields is supported:
```xml
<?xml version="1.0" encoding="utf-8"?>
<ModMetadata>
  <Name>My Mod</Name>
  <ModID>my.mod</ModID> <!-- unique id to identify mod for dependencies -->
  <Author>Me</Author>
  <Version>1.2.3</Version>
  <!-- Steam tags will automatically be converted to display proper formatting in game -->
  <Description>
    [h1]My Mod[/h1]
  </Description>
  <!-- Text for the Change Notes tab on the workshop. Should be replaced completely for each version -->
  <ChangeLog>
    [h3]Version 1.2.3[/h3]
    [list]
      [*]Fixed something
      [*]Added something else
    [/list]
  </ChangeLog>
  <WorkshopHandle>12345678</WorkshopHandle>
  <Tags><Tag>Special</Tag></Tags>
  <!-- List dependencies of this mod. Can be referenced by ModID or WorkshopHandle -->
  <DependsOn ModID="other.mod" />
  <DependsOn WorkshopHandle="87654321" />
  <!-- Ordering constraints are enforced if a matched mod is installed, but does not make them a dependency -->
  <!-- Ensure this mod is loaded before other mods -->
  <OrderBefore ModID="later.mod" />
  <!-- Ensure this mod is loaded after other mods -->
  <OrderAfter ModID="earlier.mod" />
</ModMetadata>
```

### Deprecated StationeersMods
There is also a set of deprecated fields that are still supported by StationersLaunchPad. The newer format is encouraged for readability.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ModMetadata>
  <Name>My Mod</Name>
  <Author>Me</Author>
  <Version>1.2.3</Version>
  <Description>
    [h1]My Mod[/h1]
  </Description>
  <!-- Separate description displayed in-game on workshop menu using TextMeshPro formatting tags -->
  <!-- If not present, Description field will be parsed and converted from steam to TMP format -->
  <InGameDescription>
    <![CDATA[
      <size="30">My Mod</color>
      </size>
    ]]>
  </InGameDescription>
  <ChangeLog>
    [h3]Version 1.2.3[/h3]
  </ChangeLog>
  <WorkshopHandle>12345678</WorkshopHandle>
  <Tags><Tag>Special</Tag></Tags>
  <!-- Dependencies of this mod -->
  <Dependencies>
    <Mod>
      <!-- workshop handle of dependency -->
      <Id>87654321</Id>
    </Mod>
  </Dependencies>
  <!-- Mods to load *After* this mod -->
  <!-- Equivalent to OrderBefore -->
  <LoadAfter>
    <Mod><Id>76543218</Id></Mod>
  </LoadAfter>
  <!-- Mods to load *Before* this mod -->
  <!-- Equivalent to OrderAfter -->
  <LoadBefore>
    <Mod><Id>65432187</Id></Mod>
  </LoadBefore>
</ModMetadata>
```