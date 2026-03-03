# `slp` Command

--8<-- "snippets/wip.md"

StationeersLaunchPad adds the `slp` command to the in-game console (`-slp` as launch argument) with utility commands. On the StationeersLaunchPad startup menu (when AutoLoad is disabled), the subcommands can be entered as commands without the `slp` prefix

## Commands
### `modpkg`
```
slp modpkg
```
Exports a mod package zip file containing the currently enabled mods and a modconfig.xml loading them in the current order.

### `logs`
```
slp logs
```
Shows the standalone mod logs window that allows you to view logs sent by mods.

### `config`
Contains commands for viewing and setting StationeersLaunchPad configuration from the console.

#### `list`
```
slp config list [<search>]
```
Lists configurations matching the given search text (or all configurations if no search is provided).

#### `set`
```
slp config set <name> <value>
```
Sets a configuration to the given value

### `exit`
```
slp exit
```
Exits the game immediately. This is equivalent to the base game `quit` command, but is included so it can be used on the startup menu, or as part of launch arguments.
