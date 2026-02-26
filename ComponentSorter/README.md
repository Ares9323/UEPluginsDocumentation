![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/ComponentSorter/Images/Logo.png)

# ComponentSorter
Automatically sorts the component hierarchy in the Actor and Blueprint editors alphabetically, bringing order to the chaos of randomly arranged components.

Available on [FAB](https://www.fab.com/portal/listings/bd2419db-ebae-488b-b241-5eadd8b2f1b1)


## How to activate on a single project
* Open plugins
* Look for Component Sorter
* Activate the checkbox
* Restart the editor

# How to activate globally
* Open the Unreal Engine installation folder (e.g., `C:\Program Files\Epic Games\UE_5.7\Engine\Plugins\Marketplace\ComponentSorter`)
* Open the `ComponentSorter.uplugin` file in a text editor
* Change the `EnabledByDefault` property to `true`
* Change the `Installed` property to `false` to avoid showing the plugin in the project plugins list

## The Problem

Every time you add components to an Actor or Blueprint in Unreal Engine, they appear in an unpredictable order in the Components panel. This happens because the engine gathers components from internal data structures that don't preserve insertion order, resulting in a seemingly random arrangement that gets worse as your Actor grows in complexity. Finding a specific component in a list of dozens becomes a frustrating needle-in-a-haystack experience.

## The Solution

Component Sorter is a lightweight, zero-configuration editor plugin that automatically sorts your component hierarchy alphabetically using **natural sort order**. Just install it and your components are sorted — no buttons to click, no settings to configure.

### Natural Sort Order

Unlike basic alphabetical sorting where "StaticMesh10" would appear before "StaticMesh2", Component Sorter uses natural sorting that understands embedded numbers:

```
StaticMesh1
StaticMesh2
StaticMesh3
...
StaticMesh10
StaticMesh11
StaticMesh12
```

## Features

- **Automatic sorting** — Components are sorted the moment you select an Actor or open a Blueprint, with no manual intervention required
- **Natural sort order** — Numbers in component names are compared numerically, not character-by-character
- **Respects hierarchy** — Parent-child attachment relationships are fully preserved; only sibling components at each level are reordered
- **Respects scene/non-scene separation** — The engine's separator between Scene Components and Non-Scene Components is maintained
- **Works everywhere** — Sorts in both the Level Editor Details panel and the Blueprint Editor component tree
- **Event-driven** — Only runs when something changes (selection, component added/removed, Blueprint compiled, map change), not every frame
- **Non-destructive** — Only affects the visual display order in the editor panel; does not modify your Actors, Blueprints, or any saved data
- **Zero configuration** — No settings, no menus, no UI. Install and forget
- **Case-insensitive** — "audioComponent" and "AudioComponent" sort next to each other
- **Custom order sorting logic** — Up to 10 presets available from the context menu, infinite possibilities assigning a CustomSort_X integer tag to components
