# `slp` Command in v0.3

--8<-- "snippets/wip.md"

In StationeersLaunchPad 0.3 (the repo hosted mods update), a number of additional commands have been added to interact with mod repos, as well as more general utility commands. `slp` commands will now wait for the game to be loaded to the required stage for the command, and will always be executed in order (async commands like installing repo mods will block future commands until the operation finishes).

## Commands
The following commands are in addition to the [existing commands](commands.md) supported in 0.2. When executing commands from the startup menu, omit the `slp` prefix.

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
Lists connected mod repos, with an optional search filter

#### `add`
```
slp repos add <RepoURL> [novalidate]
```
Adds a mod repo with the given http url of a `modrepo.xml` file. This makes mods in this mod repo available for installation. The optional `novalidate` argument will still add the repo even if the initial fetch of the `modrepo.xml` file fails.

For mods hosted in a github repository, you can use the base repo url and it will automatically convert it to fetch the `modrepo.xml` from the `modrepo` branch

??? example
    ```
    slp repos add github.com/RepoOwner/RepoName
    ```

#### `remove`
```
slp repos remove <RepoID|Index>
```
Removes a connected mod repo by ID (url) or by index (shown in `slp repos list`). Any mods installed from this repo will no longer update to the latest available version.

#### `update`
```
slp repos update <RepoID|Index>
```
Fetches an updated list of available mod versions from the repo specified by ID or index. When the `RepoCheckUpdates` configuration option is enabled (on by default), this will occur automatically on startup.

#### `updateall`
```
slp repos updateall
```
Fetches an updated list of available mod versions from all connected repos. When the `RepoCheckUpdates` configuration option is enabled (on by default), this will occur automatically on startup.

#### `index`
```
slp repos index [mod=<ModID>] [repo=<RepoID>] [branch=<Branch>] [version/minversion/maxversion=<Version>]
```
Lists available mod versions from connected repos. The optional arguments can be used to filter down the reuslts.

### `repomods`
Contains commands for viewing and managing installed repo mods

#### `list`
```
slp repomods list
```
Lists mods that are currently installed from a mod repo

#### `add`
```
slp repomods add <ModID> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
Installs a mod from connected repos by ModID. If not specified, `branch` will be the default (empty) branch, and version will be the latest available. If a mod is provided by multiple connected mod repos, you must specify the repo to install from.

#### `remove`
```
slp repomods remove <ModID|Index> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
Uninstalls a mod currently installed from a mod repo by ModID or index (show in `slp repomods list`). The optional parameters are used for disambiguation.

#### `update`
```
slp repomods update <ModID|Index> [version=<Version>] [branch=<Branch>] [repo=<RepoID>]
```
Updates a mod installed from a repo to the latest available version in that repo. The optional parameters are used for disambiguation.

#### `updateall`
```
slp repomods updateall
```
Updates all mods installed from a repo to the latest available version. When the `RepoModCheckUpdates` configuration option is enabled (on by default), this will happen automatically on startup.

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