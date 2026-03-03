# `slp` Command in 0.3

--8<-- "snippets/wip.md"

In StationeersLaunchPad 0.3 (the repo hosted mods update), a number of additional commands have been added to interact with mod repos, as well as more general utility commands. `slp` commands will now wait for the game to be loaded to the required stage for the command, and will always be executed in order (async commands like installing repo mods will block future commands until the operation finishes).

## Commands
The following commands are in addition to the [existing commands](commands.md) supported in 0.2

### `modpkg`
```
slp modpkg [<path.zip>]
```

The `modpkg` command now accepts an optional path to save the zip file. Omitting this argument will default to saving a timestamped zip file to `Documents/my games/Stationeers/`.

### `selfupdate`
```
slp selfupdate [<tag>] [force]
```
Updates StationeersLaunchPad to the specified tag version (or latest if omitted). Adding a `force` argument to the command will cause StationeersLaunchPad to always update, even if updating to the same or a previous version.

### `debugpkg`
```
slp debugpkg [<path.zip>]
```
Generates a debug package zip file that collects various information useful for debugging. This includes logs (the player.log as well as the in-game console log), installed mods, loaded assemblies, harmony patches, prefabs, recipes, and more. This command can be run at any point, but will not include mod assemblies and patches until mods are loaded, and will not include prefabs or recipes until the game data is loaded.

!!! tip
    When reporting an issue with StationeersLaunchPad or a mod, include this zip file to speed up diagnosing and resolving the issue.

### `repos`
Contains commands for viewing and managing connected mod repos.

#### `list`
```
slp repos list [<searchtext>]
```
#### `add`
```
slp repos add <RepoURL> [novalidate]
```
#### `remove`
```
slp repos remove <RepoID|Index>
```
#### `update`
```
slp repos update <RepoID|Index>
```
#### `updateall`
```
slp repos updateall
```
#### `index`
```
slp repos index [mod=<ModID>] [repo=<RepoID>] [branch=<Branch>] [version/minversion/maxversion=<Version>]
```
### `repomods`
Contains commands for viewing and managing installed repo mods

#### `list`
```
slp repomods list
```
#### `add`
```
slp repomods add <ModID> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
#### `remove`
```
slp repomods remove <ModID|Index> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
#### `update`
```
slp repomods update <ModID|Index> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
#### `updateall`

### `loadto`
```
slp loadto (config|mods|gamedata)
```

Waits for the game to load to the specified stage before running the following commands.

- `config` waits for the mod configuration to be loaded (the list of installed mods, the mods themselves will not be loaded yet)
- `mods` waits for the enabled mods to be loaded and initialized
- `gamedata` waits for the game to load in all prefabs and xml data

This is primarily useful as a launch argument to wait for more information to be available before creating a debug package. Most commands will automatically wait for the necessary stage before running.

??? example
    ```
    rocketstation.exe -slp loadto gamedata -slp debugpkg -slp exit
    ```