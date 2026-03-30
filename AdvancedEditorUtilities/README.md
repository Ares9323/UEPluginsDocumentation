![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/Logo.png)

# AdvancedEditorUtilities
Widgets and Utilities to improve your daily workflow in Unreal Engine
Available on [FAB](https://www.fab.com/listings/ee6ed5e0-75ae-4390-81a4-e983776eb0e7)


## How to activate
* Open plugins
* Look for AdvancedEditorUtilities
* Activate the checkbox
* Restart the editor
* [OPTIONAL], if you want to enable it by default for every project, go to `Engine\Plugins\Marketplace\AdvancedEditorUtilities` and edit `AdvancedEditorUtilities.uplugin` by adding `"EnabledbByDefault": true,` and setting `"Installed": false,` if you don't want it to show up in the .uproject file

## How to use

### Open file in windows explorer
* Select a file in content browser
* Press CTRL + ALT + E to open it in windows explorer
* [NOTE] If you select multiple files it will open all the respective folders at once

### Activate the main widget
* Click the extension button in the top bar (or press CTRL + ALT + SHIFT + E) to focus the main utility widget and run it (The shortcut could be changed or removed in Editor Settings)
* Right click any widget in the "Containers" folder and select `Run Editor Utility Widget` to open it, if you don't want to use the main widget but only a part of it.
* Drag the window wherever you want, resize it, you can even snap it into the editor layout (as you can see in the Marketplace Pictures)

### Restore Last Closed Tab (Ctrl + Shift + T)
* Press **Ctrl + Shift + T** to reopen the last asset tab you closed, similar to browser tab restore
* You can also save all currently open tabs as a **Tab Group** using the toolbar dropdown, and restore them later with **Ctrl + Shift + Alt + T**

### Capture Nodes (Ctrl + Shift + Alt + U)
* Select nodes in a Blueprint or Material graph and press **Ctrl + Shift + Alt + U** to take a high-resolution screenshot of the selected nodes

### Viewport mode selector
* Click any button under "Viewport modes" to change the current Viewport Mode, if you click the already highlighted one it will go back to the default viewport mode (By default it's "Lit" but you can change it in the `AEU_ViewModes` Widget. This works both in the editor and during play, but if you press play you have to select the viewport mode another time, because they are handled separately by the engine.

### Console Command Launcher
* Click any button under "Commands" to activate one of the default console commands
* [WARNING] Not every button works while the game is not running or while it is, some commands are specific and this doesn't depend from this plugin.
* There are 5 types of button:
  * **Toggle** - Used for commands that toggle themselves on and off if called multiple times, like `Show Collision`
  * **MultiToggle** - Used for commands that have multiple parameters activable at the same time, like `Stat` that supports `Stat FPS`, `Stat Unit`, et cetera
  * **ToggleInverse** - Used when the command used to activate the state is different from the one used to deactivate it, like `EnableAllScreenMessages` and `DisableAllScreenMessages`, in this case the first parameter in the array is used to store the second ommand.
  * **SinglePress** - Used when the command is just a single action that doesn't change the button state, like `HighResShot`
  * **RadioButton** - Used when the command has multiple parameters that can't be activated at the same time, like `Slomo` or `MaxFPS`

### Editing default settings
* You can find the settings for this plugin in the Editor Preferences - Advanced Editor Utility Plugin (Red rectangles)
* * Use the reset checkboxes (Light blue rectangle) to reset the default values of the respective category (This is needed because UPROPERTIES with the "Config" specifier don't have the default yellow icon to reset them after you edit them)

![EditorPreferences](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/EditorPreferences.png)

* You can hide unwanted ViewModes or Commands by editing the arrays in `Editor Settings/Advanced Editor Utility Plugin`(See picture below), by toggling the option `Display in Widget` (Red rectangles) or simply deleting the value.

![DisplayInWidget](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/DisplayInWidget.png)

* You can add/edit/remove custom shortcuts for Blueprints and Material nodes from here, if you do that you'll need to restart the editor to see them working:

![ChangeShortcut](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/ChangeShortcut.png)

* You can edit the "Common strings to search" array to change the dropdown menu in the extension. Each entry has a **Text** and a **Color** field, so you can assign a distinct color to each tag (this color is also used when creating Common String Comments, see below):

![CommonStrings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStrings.png)

* You can also assign them a shortcut to launch the filter automatically:

![CommonStringsDropdown](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStringsDropdown.png) ![FindInBlueprints](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/FindInBlueprints.png)

* Changes to Common Strings are applied immediately in the dropdown menu without needing to restart the editor.

* The other settings are also changeable from here, but they can be modified through their own widgets, so I don't really recommend doing it from here:

![WidgetSettings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/WidgetSettings.png)

* You can also edit them in a permanent way, by editing the `DefaultCommands` and `DefaultViewModes` arrays in C++ by editing `AdvancedEditorUtilitiesSettings.h` (**WARNING: you need to move the plugin from the Marketplace folder into a project "Plugins" folder to recompile it, then you can move it back but you might lose your settings if you update the plugin from the Epic Launcher**)

---

### Common String Comment (Shift + Alt + C)
* While editing a Blueprint or Material graph, press **Shift + Alt + C** to open a picker popup listing all your Common Strings
* Select an entry to create a **Comment node** with that tag as text and its associated color
* If you have **nodes selected**, the comment will automatically wrap around them
* If no nodes are selected, the comment is placed at the center of the viewport
* The available entries and their colors are configured in `Editor Settings / Advanced Editor Utility Plugin` under "Common Strings to Search"

### Add Timeline Node (Shift + Alt + T)
* While editing an **Actor-based Blueprint** graph, press **Shift + Alt + T** to spawn a **Timeline node** at the mouse cursor position
* The node is created with a unique name and its corresponding `UTimelineTemplate` component, so you can double-click it immediately to open the Timeline editor
* This shortcut only works in Actor-based Blueprints (the same restriction as the native right-click menu)

### Toolbar Dropdown Sections
The AEU toolbar dropdown button is organized into labeled sections:
* **Tab Restore** — Restore Saved Tab Group, Save Open Tabs As Tab Group
* **Tools** — World Locker, Image Resizer
* **Find In Blueprints** — Dynamic entries from your Common Strings, each launching a "Find In Blueprints" search for that tag

---

## Level Design Library

A Blueprint Function Library (`UAEU_LevelDesignLibrary`) with tools for manipulating selected actors in the viewport. All functions operate on the current editor selection and support full Undo/Redo.

### Alignment
* **AlignSelectedActors** — Align all selected actors along X, Y, or Z using Min, Max, or Center mode. Requires 2+ selected actors.

### Distribution
* **DistributeSelectedActorsAlongAxis** — Space selected actors equally along an axis. First and last actors stay in place. Requires 3+ selected actors.
* **DistributeSelectedActorsRadially** — Distribute actors around a center point with configurable min/max radius, equal or random spacing, and optional orient-to-center.

### Randomizers
* **RandomizeSelectedActorsRotationZ** — Randomize yaw only (the most common case for props and foliage), with configurable min/max angle.
* **RandomizeSelectedActorsRotation** — Randomize rotation on all three axes with independent min/max per axis.
* **RandomizeSelectedActorsScale** — Randomize uniform scale with min/max range.
* **RandomizeSelectedActorsScale3D** — Randomize scale per-axis with independent min/max vectors (X, Y, Z).

### Snap to Surface
* **SnapSelectedActorsToSurface** — Line-trace from each selected actor in one of 6 directions (Down, Up, Left, Right, Forward, Backward) and snap to the hit surface. Configurable max trace distance and optional align-to-surface-normal.

### Convert to Instanced Mesh
* **ConvertSelectedActorsToInstancedMesh** — Group selected static mesh actors by mesh asset and replace them with Instanced Static Mesh actors. Option to keep or delete originals (deleted by default, kept originals are moved to a configurable folder).

---

## Mesh Socket Utilities

A Blueprint Function Library (`UAEU_BlueprintFunctionLibrary`) for batch socket operations on Static Meshes, Skeletal Meshes, and Skeletons. Also accessible via **right-click context menus** in the Content Browser on compatible asset types.

### Static Mesh Sockets
* **CopySocketsFromStaticMesh** — Copy all sockets from a source to one or more target static meshes.
* **DeleteAllSocketsFromStaticMesh** — Remove all sockets from a static mesh.
* **CreateMultipleStaticMeshSockets** — Batch-create numbered sockets with cumulative location/rotation offset.
* **ExportStaticMeshSocketsToJSON** / **ImportStaticMeshSocketsFromJSON** — Export/import sockets to/from JSON files (default filename: `{MeshName}_sockets.json`).

### Skeletal Mesh Sockets
* **CopySocketsFromSkeletalMesh** — Copy sockets between skeletal meshes. Uses the **Bone Name Resolver** (see below) to automatically remap bones across different skeleton standards.
* **DeleteAllSocketsFromSkeletalMesh** — Remove all mesh-local sockets from a skeletal mesh.
* **CreateSocketsOnMatchingBones** — Create sockets on all bones matching a wildcard pattern (e.g. `*finger*`, `hand_*`).
* **ExportSkeletalMeshSocketsToJSON** / **ImportSkeletalMeshSocketsFromJSON** — Export/import sockets to/from JSON. Exports include skeleton-inherited sockets. Import uses the Bone Name Resolver for cross-skeleton compatibility.

### Skeleton Sockets
* **CopySocketsFromSkeleton** — Copy sockets between skeletons with automatic bone name resolution.
* **DeleteAllSocketsFromSkeleton** — Remove all sockets from a skeleton.
* **ExportSkeletonSocketsToJSON** / **ImportSkeletonSocketsFromJSON** — Export/import skeleton sockets to/from JSON with bone name resolution on import.

### Content Browser Context Menus
Right-click a **Static Mesh**, **Skeletal Mesh**, or **Skeleton** asset in the Content Browser to access the **AEU Socket Utilities** section:
* **Copy Sockets from Source...** — Opens an asset picker to choose a source asset, then copies sockets to all selected targets.
* **Delete All Sockets** — Removes all sockets from the selected assets.
* **Export Sockets to JSON...** — Opens a save dialog to export sockets.
* **Import Sockets from JSON...** — Opens an open dialog to import sockets.

---

## Bone Name Resolver

When copying or importing sockets between skeletal meshes or skeletons with different naming conventions, the **Bone Name Resolver** (`UAEU_BoneNameResolver`) automatically maps bone names across standards. This is used transparently by the socket copy/import functions.

### Supported Skeleton Standards
* **UE5 Mannequin** (e.g. `pelvis`, `hand_l`, `calf_r`)
* **UE4 Mannequin** (same naming as UE5)
* **Mixamo** (e.g. `Hips`, `LeftHand`, `RightLeg`)
* **Daz3D / Genesis** (e.g. `hip`, `lHand`, `rShin`)
* **HumanIK** (e.g. `Hips`, `LeftHand`, `RightLeg`)

### Resolution Order
1. **Exact match** — Bone name exists on the target as-is.
2. **Prefix stripping** — Removes known prefixes (`mixamorig:`, `mixamorig_`, `Bip01_`, `Genesis8_`, etc.) and retries exact match.
3. **Mapping table lookup** — Looks up the bone in the mapping table (51 bone groups covering the full body and all fingers). Once the target skeleton's standard is detected, it is cached and prioritized for all subsequent lookups.
4. **Levenshtein fuzzy match** — Normalized string similarity (default threshold: 0.8) against all target bones, with prefix stripping applied.
5. **Skip with warning** — If nothing matches, the socket is skipped and a warning is logged.

### Standard Detection Caching
On the first bone lookup, the resolver scans both source and target skeletons to detect which standard they use (by counting bone name matches). The detected standards are **cached for the entire operation**, so subsequent bones skip directly to the right mapping — no need to cycle through all standards every time.

### Customization
* **Custom mapping file** — Call `SetBoneMappingFile()` from Blueprint or C++ to load a custom JSON mapping table instead of the default one.
* **Fuzzy match threshold** — Adjust `FuzzyMatchThreshold` (0.0–1.0, default 0.8) to make fuzzy matching more or less strict.
* **Mapping JSON location** — Default: `{PluginDir}/Config/BoneMapping.json`. Editable to add new skeleton standards or bone groups.
