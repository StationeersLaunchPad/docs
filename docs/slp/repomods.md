# Repo Hosted Mods

Starting in StationeersLaunchPad 0.3, mods can be installed and updated from an online repository instead of the steam workshop.

For full details on how the feature works, see the [GitHub Hosted Mods Design](https://github.com/StationeersLaunchPad/StationeersLaunchPad/issues/95).

!!! note
    Currently there is no UI in StationeersLaunchPad for interacting with repos and repo mods. Everything is managed via console commands. The UI will be built as the feature matures.

## Usage
Add a github repo to make its hosted mods available for install
```
slp repos add github.com/<user>/<repoName>
```
Or for a custom hosted repo, add the direct link to the modrepo.xml file
```
slp repos add https://example.com/modrepo.xml
```

Show mod index to see available mods and versions
```
slp repos index
```

Install a mod by ModID
```
slp repomods add my.mod
```

For full info on the supported commands, see [`slp` Command in v0.3](commands_0.3.md)

## Developer Usage
In order for a mod to be available in a mod repo, it **must** contain a `ModID` and `Version` in its `About.xml` file.

### Packaging
A mod version hosted in a repo must be a zip file (one mod per zip file) with the mod files at the root (not nested in a folder). See [Mod Structure](../modding/structure.md) for more info on mod files.
```
MyMod.zip/
  About/
    About.xml
```
### GitHub hosting
When hosting in a GitHub repo, the default location for the `modrepo.xml` file is at the root on a branch named `modrepo`.

To simplify the process of managing mod releases in a GitHub repo, use the [StationeersLaunchPad/modrepo-builder-action](https://github.com/StationeersLaunchPad/modrepo-builder-action) GitHub action by [aproposmath](https://github.com/aproposmath) to automatically build and update the `modrepo.xml` file when a GitHub release is made.

### Custom hosting
A mod repo can be hosted anywhere as long as the `modrepo.xml` and the mod version zip files are accessible via http. See the [GitHub Hosted Mods Design](https://github.com/StationeersLaunchPad/StationeersLaunchPad/issues/95) for full details on how to structure the `modrepo.xml` file.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ModRepo>
  <!-- List all available versions of mods. Digest is optional -->
  <ModVersion
    ModID="my.mod"
    Version="0.1.2"
    Name="My Mod"
    Author="me"
    Url="https://example.com/my.mod-0.1.2.zip"
    Digest="sha256:0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef"
  />
</ModRepo>
```