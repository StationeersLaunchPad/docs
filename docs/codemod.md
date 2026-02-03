# Writing a Code Mod

!!! note "Work In Progress"
    This documentation is a work in progress. Help out by submitting a pull request to the [docs repository](https://github.com/StationeersLaunchPad/docs)

!!! warning "Linking against StationeersLaunchPad"
    Linking against StationeersLaunchPad (using any class in the `StationeersLaunchPad` namespace or nested namespaces) is unsupported. These classes are not a stable API, and will change without notice. The code is MIT licensed so you are free to copy any utilities you want to use into your own mod. [LaunchPadBooster](#launchpadbooster) also contains utilities with a stable API that can be used by mods. If there is something you need that only StationeersLaunchPad has, reach out on github or discord and it can be added as an injected parameter to the Default Entrypoint.

StationeersLaunchPad will load any dll files in an enabled mod folder and search them for supported mod entrypoints. These entrypoints will be initialized on the splash screen before the primary game scene is loaded, so care must be taken to avoid accessing parts of the game that have not been properly loaded yet.

## Default Entrypoint (preferred)

Any class extending `UnityEngine.MonoBehaviour` that contains an `OnLoaded` method with at least one supported injected parameter will be treated as a mod entrypoint. It will be added as a component to a global mod GameObject and the `OnLoaded` method will be called with the injected parameters.

### Injected Parameters
The `OnLoaded` method of the entrypoint class must have at least one injected parameter, and only injected parameters. These injected parameters are found by an exact match on the type (not the parameter name). If you do not need any data injected from StationeersLaunchPad, just include a `List<GameObject> prefabs` parameter so the entrypoint can be identified.

`List<GameObject> prefabs`
:   StationeersLaunchPad automatically loads .asset files in enabled mods. This parameter will contain the list of `GameObject`s that were loaded from these asset files.

    These asset files will be loaded in regardless of whether an entrypoint is receiving them, so including this parameter does not change the loading behavior, only the data that your entrypoint receives.

`ConfigFile config`
:   When this parameter is present, StationeersLaunchPad will create a BepInEx config file using the `ModID` specified in the `About.xml` as the name (falling back to the fully qualified class name of the entrypoint class when `ModID` is not specified). Configurations registered to this config file will be visible in the StationeersLaunchPad configuration UI in the startup menu and the main menu workshop page.

This list will be expanded over time as new features are added. Each parameter is optional, so existing entrypoints will continue to be valid as more injected parameters are added.

### Example
```cs
using BepInEx.Configuration;
using System.Collections.Generic;
using UnityEngine;

public class MyMod : MonoBehaviour
{
  // Must contain one of the following instance methods
  // The method visibility and parameter names don't matter
  void OnLoaded(List<GameObject> prefabs);
  void OnLoaded(ConfigFile config);
  void OnLoaded(List<GameObject> prefabs, ConfigFile config);
  void OnLoaded(ConfigFile config, List<GameObject> prefabs);
}
```

## LaunchPadBooster
[LaunchPadBooster](https://github.com/StationeersLaunchPad/LaunchPadBooster) is a library bundled with StationeersLaunchPad that contains utilities for common tasks in mods.

## Other Entrypoints
Support for other entrypoint types is included for compatibility with existing mods.
### BepInEx
Classes extending the BepInEx `BaseUnityPlugin` class will be loaded as mod entrypoints. These are not loaded in by the BepInEx ChainLoader and as a result they will not respect BepInEx dependency and incompatibility annotations.
### StationeersMods
Classes extending the StationeersMods `ModBehaviour` class will be loaded as entrypoints. This framework is deprecated, but StationeersLaunchPad includes a compatibilty shim so mods written targeting this framework can still be used.