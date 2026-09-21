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

## Table of contents
* [Keyboard shortcuts](#keyboard-shortcuts)
* [Main widget and toolbar](#main-widget-and-toolbar)
* [View Modes and Console Commands panels](#view-modes-and-console-commands-panels)
* [Material Parameters panel](#material-parameters-panel)
* [Create PBR Textures](#create-pbr-textures)
* [Make Seamless](#make-seamless)
* [Graph editor tools](#graph-editor-tools)
* [Editor settings](#editor-settings)
* [Naming Convention](#naming-convention)
* [Auto-confirm Editor Prompts](#auto-confirm-editor-prompts)
* [World Locker](#world-locker)
* [Level Design Tools](#level-design-tools)
* [Physics Tools](#physics-tools)
* [Image Resizer](#image-resizer)
* [Folder colors and templates](#folder-colors-and-templates)
* [Content Browser context menus](#content-browser-context-menus)
* [Data Table / Data Asset conversion](#data-table--data-asset-conversion)
* [Asset editor toolbar buttons](#asset-editor-toolbar-buttons)
* [Mesh Socket Utilities](#mesh-socket-utilities)
* [Bone Name Resolver](#bone-name-resolver)
* [Blueprint and Remote Control functions](#blueprint-and-remote-control-functions)

---

## Keyboard shortcuts
Every entry is an editor command, so it can be rebound or assigned in `Editor Preferences > Keyboard Shortcuts` (search for "Advanced Editor Utilities"). Commands listed without a default chord have none until you assign one.

| Command | Default | Where it works |
|---|---|---|
| Open A.E.U. Utility | Ctrl + Shift + Alt + E | Everywhere |
| Show in Explorer | Ctrl + Alt + E | Content Browser selection |
| Restore Last Closed Tab | Ctrl + Shift + T | Everywhere |
| Restore Saved Tab Group | Ctrl + Shift + Alt + T | Everywhere |
| Save Open Tabs As Tab Group | none | Everywhere |
| Capture Nodes | Ctrl + Shift + Alt + U | Any graph editor |
| Create Common String Comment | Shift + Alt + C | Blueprint / Material graphs |
| Add Timeline | Shift + Alt + T | Actor-based Blueprint graphs |
| Add Math Expression | Ctrl + Alt + M | Blueprint graphs |
| Update Redirector References | none | Content Browser selection (or `/Game` when nothing is selected) |
| Select Actors Using This Asset | none | Content Browser selection |
| Select Actors Using The Same Mesh | none | Viewport selection |
| Select Actors Using The Same Material | none | Viewport selection |
| Disable/Enable Selection, Disable/Enable Movement, Enable Selection for All, Enable Movement for All | none | Viewport selection (World Locker) |
| Pause Auto-confirm Editor Prompts | none | Everywhere |
| Cancel Physics Drop | Esc | While a live drop or array preview is running |
| Level Design Tools (`LDT_*`): Align, Distribute, Snap, Move/Rotate/Scale ± step, Randomize, Cycle Transforms, Array Grid/Radial/Scatter/Spline, Confirm/Cancel Array, Physics Drop Live/Confirm/Cancel, Pivot Actor and Source Actors, Rename Selected Actors | none | Viewport selection |

---

## Main widget and toolbar

### Open file in windows explorer
* Select a file in content browser
* Press CTRL + ALT + E to open it in windows explorer
* [NOTE] If you select multiple files it will open all the respective folders at once

### Activate the main widget
* Click the extension button in the top bar (or press CTRL + ALT + SHIFT + E) to focus the main utility widget and run it (The shortcut could be changed or removed in Editor Settings)
* Right click any widget in the "Containers" folder and select `Run Editor Utility Widget` to open it, if you don't want to use the main widget but only a part of it.
* Drag the window wherever you want, resize it, you can even snap it into the editor layout (as you can see in the Marketplace Pictures)
* The main widget is organized in tabs, and the last active tab is remembered between sessions: **Viewport** (view modes), **Console** (console commands), **Renamer**, **Align**, **Array**, **Pivot**, **Random** (see [Level Design Tools](#level-design-tools)) and **Outliner** (World Outliner organizer: a class-to-folder map in the settings, **Organize World Outliner** moves every actor into the folder of its class, selected actors first)

### Restore Last Closed Tab (Ctrl + Shift + T)
* Press **Ctrl + Shift + T** to reopen the last asset tab you closed, similar to browser tab restore
* You can also save all currently open tabs as a **Tab Group** using the toolbar dropdown, and restore them later with **Ctrl + Shift + Alt + T**

### Toolbar Dropdown Sections
The AEU toolbar dropdown button is organized into labeled sections:
* **Tab Restore**: Restore Saved Tab Group, Save Open Tabs As Tab Group
* **Tools**: World Locker, Image Resizer, View Modes, Console Commands, Material Parameters (each opens as a dockable tab, and each has its own switch in Menus & Toolbars for anyone who already has these panels inside their own utility widget; the tabs stay reachable from the Window menu either way)
* **Find In Blueprints**: dynamic entries from your Common Strings, each launching a "Find In Blueprints" search for that tag. Every entry is marked with a dot in the colour configured for that tag, the same one its comment nodes get, so the dropdown doubles as their legend (the Common String Comment picker, Shift + Alt + C, shows the same dots)

The `Tools` main menu also gains an **Advanced Editor Utilities** section with the **Starship Style Gallery** (browse every editor icon, brush, color and style, handy when building your own tools).

---

## View Modes and Console Commands panels
Both panels exist as tabs of the main widget and as standalone dockable windows (toolbar dropdown > Tools). They are native Slate panels built from the entries configured in the plugin settings.

### View Modes
* Click any button to change the current Viewport Mode; click the highlighted one again to go back to the default view mode ("Lit" by default, configurable). The list includes every engine view mode plus the visualization sub-targets (buffer visualization, Nanite, Lumen, Virtual Shadow Maps, and so on), aligned with the engine version you are running.
* This works both in the editor and during play, but if you press play you have to select the view mode another time, because they are handled separately by the engine.
* Entries are grouped in **collapsible categories**; which categories you folded is remembered between sessions.
* A **search box** filters the list.
* Hover an entry and click the **eye** to hide it; hidden entries are remembered and can be shown again with the "show hidden" toggle at the top of the panel.

### Console Commands
* Click any button to run one of the configured console commands
* [WARNING] Not every button works while the game is not running or while it is, some commands are specific and this doesn't depend from this plugin.
* Same search, categories and hide-with-the-eye behaviour as the View Modes panel.
* There are 5 types of button:
  * **Toggle**: used for commands that toggle themselves on and off if called multiple times, like `Show Collision`
  * **MultiToggle**: used for commands that have multiple parameters activable at the same time, like `Stat` that supports `Stat FPS`, `Stat Unit`, et cetera
  * **ToggleInverse**: used when the command used to activate the state is different from the one used to deactivate it, like `EnableAllScreenMessages` and `DisableAllScreenMessages`, in this case the first parameter in the array is used to store the second command.
  * **SinglePress**: used when the command is just a single action that doesn't change the button state, like `HighResShot`
  * **RadioButton**: used when the command has multiple parameters that can't be activated at the same time, like `Slomo` or `MaxFPS`

---

## Material Parameters panel
A dockable window (toolbar dropdown > Tools > **Material Parameters**) listing the materials used by the **selected actors**, with the parameters of every Material Instance editable in place. Like the View Modes and Console Commands panels it is also a UMG widget, under the **Advanced Editor Utilities** palette category, so you can drop it into an Editor Utility Widget of your own. It follows the viewport selection, so it is the fastest way to tweak a scene without opening one Material Instance editor per object.

* Parameters keep the **order the material declares them in**, grouped by their authored groups; the parameters a material left ungrouped end up in "Global". Alphabetical sorting would scramble the "01 - BaseColor / 02 - Textures" layouts materials are usually authored with.
* Each row has the **override checkbox** of the Material Instance editor, the value editor for its type (scalar slider, colour swatch, texture picker, static switch...) and a **reset arrow** shown only while the instance overrides its parent.
* One **search box** at the top filters the parameters of every material at once. Next to it, two buttons fold or unfold **General** and **Used by** across all of them; both start folded.
* **Used by** lists every actor, component and material slot of the selection using that material, and clicking one selects that actor alone.
* **General** is the instance's physical material, Lightmass settings and base property overrides, shown with the engine's own editors.
* A plain **Material** (not an instance) still gets a row: its parameters cannot be edited, but "Create child instance" turns it into one and assigns it to the selection on the spot.
* Edits are written straight to the asset, exactly like the Material Instance editor does, and they are **undoable** (a slider drag or a colour picker drag is one undo step). If that editor is open on the same instance, its checkboxes and values follow along.

The buttons on each material's title bar, left to right:

| Button | What it does |
|---|---|
| **Save** | Saves the material. Shown only while the asset is dirty; it is not an "apply", every edit already went into the asset |
| **Revert** | Discards the unsaved parameter changes by reading back the version on disk. Nothing is unloaded (unlike `Asset Actions > Reload`), so no reference anywhere goes stale, and the revert itself is undoable. Shown only while the asset is dirty |
| **Use Selected Asset from Content Browser** | Replaces this material with the one selected in the Content Browser, in every slot of the selection that was using it |
| **Show in Content Browser** / **Open** | Browse to the asset, or open it in its own editor |
| **Select actors using this material** | Selects every actor in the loaded levels using it, not just the ones already selected |
| **Duplicate as sibling** | Duplicates the instance (same parent, same overrides) and assigns the copy wherever the selection used the original |
| **Create child instance** | Creates a child Material Instance and assigns it the same way. The only entry available on a plain Material |
| **Check all / Uncheck unchanged** | The checkbox at the end: checked, it overrides every parameter of the instance; unchecked, it drops only the overrides whose value still equals the parent's, so nothing you actually changed is lost. One transaction either way, and the same action sits in the Material Instance editor toolbar |

Both creation buttons save the new instance to disk as soon as they assign it, so Revert has a saved state to go back to from the very first edit.

Two settings live in `Editor Preferences > Advanced Editor Utilities > Advanced Settings`: the **maximum number of materials** the panel lists at once (a select-all would otherwise build hundreds of rows), and a list of **excluded materials** by name or path, wildcards allowed. The General section can also be turned off there.

---

## Create PBR Textures
Right-click a colour texture and pick **Create PBR Textures...**, or open the panel from `Window` and drop a texture on it. The panel shows the source beside the maps estimated from it, framed together, each with its own parameters underneath.

Everything here is a guess read out of the luminance of the source: a normal from its gradient, an occlusion from the horizon around each pixel, a roughness from local contrast, an albedo from flattening the light the photo baked in. They are not measurements, and no colour image carries the information a scanner would give you. Good enough to block out a material or to rescue a texture that came with nothing else, not a replacement for authored maps.

* The source has to be a **colour texture**. Anything whose name ends with a suffix from the ignore list, or that is compressed as a normal map, a mask or a grayscale, is left out of the picker and out of the menu entirely, rather than silently producing a normal of a normal.
* Tick the maps you want: **Normal**, **Roughness**, **Ambient Occlusion**, **Metallic**, **ORM**, **Albedo**, **Height**, **Edge**. Each becomes a column, in a fixed order so a column never moves when another is switched off.
* **ORM (packed)** puts occlusion in red, roughness in green and metallic in blue. While it is on, those three maps are switched off on their own: shipping both the packed texture and its three halves is what packing them was meant to avoid.
* Zoom with the wheel, pan by dragging, double click to frame it all. Every column shows the same crop, which is the only way to compare them.
* Each column has its own **Resolution** for the file it writes, from the source's size down to 128, and its own Create button. An existing map with that name is rewritten in place, so the materials pointing at it keep working.
* **Realtime update** (off by default) re-estimates while a slider is dragged instead of when it is released.

### Bringing your own maps
`Height in` and `Normal in` take a height or a normal you already have, and they are worth more than every estimator in the panel: an occlusion or a curvature read off a real normal is a calculation, the same thing read off an invented one is only plausible. With a height supplied the bands below are bypassed; with a normal supplied and no height, the height is recovered from it by integrating its gradients.

### The maps
| Map | What it reads | Notes |
|---|---|---|
| **Height** | Five bands of detail, an octave apart, each with its own weight (fine, small, medium, large, base) | This is the relief every other map is read from. Base at zero keeps the shapes and throws away the slow shading, which on a photo is usually light and not form |
| **Normal** | The gradient of that height | Strength is exponential: the useful range on a soft surface is under 1 and on a carved one is in the tens |
| **Ambient Occlusion** | Eight horizons traced around each pixel over the height | Not "this pixel is darker than its neighbours": a dark speck painted on a flat surface has no horizon above it and stays unoccluded |
| **Roughness** | Local contrast around a base value | |
| **Metallic** | How close each pixel is to a colour you pick with the eyedropper, measured in hue, saturation and value | Metal cannot be read out of brightness: a metal band and a pale stripe of paint look the same to a luminance estimator |
| **Albedo** | The source with its illumination flattened | Handles a gradient, not a hard shadow |
| **Edge** | Curvature of the normal field | Bright on convex edges, dark in crevices, grey where flat: the mask for edge wear and for dirt |

### The material
**Material** at the end of the second row decides what `Create All Shown` does once the maps exist:
* **New material**: a material next to the source with the maps on texture **parameters** named `BaseColor`, `Normal`, `Roughness`, `Metallic`, `AmbientOcclusion`, `ORM`, `Height`, `Edge`, wired to the right inputs with the right sampler types. Parameters and not baked samples, because a material with its textures fixed in cannot be instanced. Roughness goes through a `Roughness Multiplier` scalar, so an instance can dial the whole surface without touching the texture.
* **Instance of a parent**: pick a material you already have and the maps are matched to its texture parameters by name, trying the usual spellings first exactly and then loosely (`BaseColor`, `Albedo`, `Diffuse`; `Normal`, `NormalMap`; `ORM`, `MRA`, `MaskMap`...). A map that finds no parameter is named in the status line rather than dropped in silence. The instance is reused when it exists, so running it twice updates instead of leaving `MI_Foo_1` behind.

Every texture written carries `AEU.Estimated`, `AEU.EstimatedFrom` and `AEU.Origin` in its metadata (`Asset Actions > Show Metadata`), so months later nobody has to wonder whether a normal came out of a scanner or out of a guess.

The suffixes, the ignore lists, the preview size and the default parameters live in `Editor Preferences > Advanced Editor Utilities > Advanced Settings`, under **Texture to PBR**.

---

## Make Seamless
Right-click a texture and pick **Make Seamless...**. The panel shows the texture as it is beside the result, both drawn **repeated**, because a single copy of a texture always looks fine and the seam only exists where two copies meet.

Two different problems, handled in this order:
* **Level Lighting** flattens the slow brightness variation across the image. This is the half nobody expects: if one side of the photo was lit brighter than the other, the tiled result shows a band at every repeat however well the seam itself is blended. The correction divides by the local level instead of subtracting it, so the material keeps its contrast, and **Level Radius** says what counts as slow.
* Then the seam, in one of two modes. **Blend the seam** offsets the image by half so the two joins land in the middle, where there is material around them to blend with, and mixes in the copy from the other side over a band you set. **Mirror** always tiles by construction, at the price of a symmetry the eye finds quickly.

It does not invent detail: a structured pattern, a brick course or a plank, will still show where it repeats. That needs synthesis rather than blending, and is not what this does. The result is written as `<Name>_Tiling` next to the source, keeping its compression and colour space.

---

## Graph editor tools

### Capture Nodes (Ctrl + Shift + Alt + U)
* Select nodes in a Blueprint, Material, Niagara or any other node graph and press **Ctrl + Shift + Alt + U** to take a high-resolution screenshot of the selected nodes (saved under `Saved/Screenshots/GraphScreenshots`)
* The same action is available as a **Capture Nodes** button in the toolbar of every asset editor that has a graph; the button is not shown on assets without one (Data Assets, textures, meshes...)
* The zoom level used for the capture is configurable in the settings (`Graph Screenshot`), from 1:1 up to the engine's maximum zoom

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

### Add Math Expression Node (Ctrl + Alt + M)
* While editing a Blueprint graph, press **Ctrl + Alt + M** to spawn a **Math Expression** node at the mouse cursor position
* The default expression it opens with is configurable in the settings

### Node shortcuts
* You can add/edit/remove custom shortcuts for Blueprint and Material nodes from the settings; if you do that you'll need to restart the editor to see them working:

![ChangeShortcut](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/ChangeShortcut.png)

---

## Editor settings
* The settings live in `Editor Preferences` under their own **Advanced Editor Utilities** category, not inside Plugins, split into one page per topic so the big arrays never crowd each other: **Advanced Settings** (restore all, graph screenshot zoom, auto-confirm prompts, Material Parameters options, and the on/off switch of every menu entry and toolbar button the plugin adds), **Console Commands**, **View Modes**, **Common Strings**, **Node Shortcuts**, **Naming Convention**, **World Outliner**, **Folder Templates**. They all edit the same settings object, so nothing changes in how they are saved (the pictures below still show the older single page). In every page the plain options come first and the long arrays last, with each array's reset checkbox above it.
* **Context Menu Placement** decides where the plugin's section goes inside the Content Browser menus: bottom (the default, where a menu extension lands on its own), top, or before / after a section you name in **Context Menu Anchor Section** (`CommonAssetActions` is the Edit / Rename / Duplicate block, `ImportedAssetActions` the Reimport one). An unknown name falls back to the bottom.
* The category sits right below **General**. If you would rather have it elsewhere in the list, `Settings Category Sort Priority` in Advanced Settings moves it (lower goes higher up; the engine's own categories all sit at 0, except Advanced at 1).
* The Level Design settings (arrays, physics tools, renamer, steps...) are per-project and live in `Project Settings > Plugins > AEU Level Design Settings`.
* Use the reset checkboxes (Light blue rectangle) to reset the default values of the respective category (This is needed because UPROPERTIES with the "Config" specifier don't have the default yellow icon to reset them after you edit them)

![EditorPreferences](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/EditorPreferences.png)

* You can hide unwanted ViewModes or Commands by editing the arrays in `Editor Settings/Advanced Editor Utility Plugin`(See picture below), by toggling the option `Display in Widget` (Red rectangles) or simply deleting the value. For a quicker per-user hide, use the eye icon directly in the panels.

![DisplayInWidget](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/DisplayInWidget.png)

* You can edit the "Common strings to search" array to change the dropdown menu in the extension. Each entry has a **Text** and a **Color** field, so you can assign a distinct color to each tag (this color is also used when creating Common String Comments):

![CommonStrings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStrings.png)

* You can also assign them a shortcut to launch the filter automatically:

![CommonStringsDropdown](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStringsDropdown.png) ![FindInBlueprints](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/FindInBlueprints.png)

* Changes to Common Strings are applied immediately in the dropdown menu without needing to restart the editor.

* The other settings are also changeable from here, but they can be modified through their own widgets, so I don't really recommend doing it from here:

![WidgetSettings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/WidgetSettings.png)

* The global settings (commands, view modes, common strings, node shortcuts, naming convention, auto-confirm, outliner palette) are stored in `Settings.ini` inside the plugin folder, so they follow the plugin across projects. The Level Design settings are per-project editor settings.
* You can also edit them in a permanent way, by editing the `DefaultCommands` and `DefaultViewModes` arrays in C++ by editing `AEU_Settings.h` (**WARNING: you need to move the plugin from the Marketplace folder into a project "Plugins" folder to recompile it, then you can move it back but you might lose your settings if you update the plugin from the Epic Launcher**)

---

## Naming Convention
A class-to-prefix map (`StaticMesh` → `SM_`, `Blueprint` → `BP_`, `Texture2D` → `T_`, `DataTable` → `DT_`, `DataAsset` → `DA_`, `UserDefinedStruct` → `F_`, and about 80 more) drives every rename feature. Blueprints are resolved by their parent class, so a Blueprint deriving from `GameModeBase` gets `GM_`.

* **Adapt To Naming Convention**: right-click any selection in the Content Browser to rename it to the convention. Known prefixes are stripped first, so `Foo_SM` or `BP_Foo` selected as a Material Instance both become `MI_Foo`. The currently open level is skipped. Classes without a prefix are listed in a notification so you can add them.
* **Auto adapt on import** / **Auto adapt on creation** (both off by default): rename assets automatically as soon as they are imported from disk or created in the editor (only under `/Game`, redirectors excluded). Automation runs (commandlets, unattended sessions, automation tests) never trigger the rename.
* **Strip auto-generated suffixes**: removes `_Montage`, `_Composite`, `_PoseAsset`, `_Physics`, `_Inst` and similar suffixes the engine appends.
* **Auto-generate prefix from class name**: for classes not in the map, build a prefix from the uppercase letters of the class name (`ForceFeedbackEffect` → `FFE_`).
* The map is editable in the settings (`Naming Convention`) and can be reset to the defaults with its reset checkbox.

---

## Auto-confirm Editor Prompts
Off by default. When enabled, the plugin scans the top-level windows once per second and clicks through recurring confirmation dialogs for you:
* the "Source code, config INI, and text files may need Find/Replace" prompt shown when renaming or moving assets referenced from non-asset files
* the "Confirm loading N assets" prompt shown once per folder when copying or loading large asset sets

Each prompt can be enabled individually, and the **Pause Auto-confirm Editor Prompts** command pauses the scanner without touching the settings.

---

## World Locker
A dockable tab (toolbar dropdown > Tools > World Locker) that lists the actors of the loaded levels in a tree with two lock columns:
* **Selection lock**: the actor can no longer be selected in the viewport (handy for floors, walls and backdrops you keep clicking by mistake)
* **Movement lock**: the actor can be selected but not moved

Locks are stored as actor tags (`AEU_SelectionDisabled`, `AEU_MovementDisabled`), so they survive even when the plugin is not loaded and travel with the level. The same two columns are added to the native **World Outliner**, and the lock state can also be toggled from the outliner right-click menu (**Advanced Editor Utilities** section) or with the assignable commands. **Enable Selection for All** / **Enable Movement for All** clear every lock in one go. Non-editable actors are hidden from the tab.

### Actor colors
* Right-click actors in the outliner (or in the World Locker tab) > **Set Color** to tint them with a palette entry, **Custom Color...** for any color, or **Clear Color**.
* The color is stored as an actor tag (`AEU_Color_<PaletteName>` or `AEU_Color_RRGGBB`), so it works in packaged tools and version control as well. It tints the actor label in the World Locker tab and the lock icons in the native outliner.
* The palette is editable in the settings (`Outliner Color Palette`).
* **Class tag mappings** (settings): assign a tag to a class (for example a color to every `Light`) without touching the actors; every instance of that class and its subclasses is treated as if it carried the tag.

---

## Level Design Tools
The Renamer, Align, Array, Pivot and Random tabs of the main widget, backed by the `UAEU_LevelDesignLibrary` Blueprint Function Library and by mappable `LDT_*` commands. Everything operates on the current viewport selection, supports full Undo/Redo, and also works on the instances of selected Instanced Static Mesh components. Parameters live in the per-project `Level Design` settings so every tab and shortcut shares them.

### Alignment and distribution
* **Align**: align the selected actors along X, Y or Z using Min, Max or Center, optionally using bounds instead of pivots. Requires 2+ actors.
* **Distribute along axis**: space the selected actors equally along an axis, first and last stay in place. Requires 3+ actors.
* **Distribute radially / around the Pivot Actor**: distribute around a center point with configurable min/max radius, equal or random spacing, and optional orient-to-center.

### Snap to surface
* Line-trace from each selected actor in one of 6 directions (Down, Up, Left, Right, Forward, Backward) and snap it to the hit surface. Configurable max trace distance and optional align-to-surface-normal.

### Transform steps
* **Move ±X/Y/Z**, **Rotate ±Roll/Pitch/Yaw**, **Scale ± (uniform or per axis)** nudge the selection by the Location / Rotation / Scale steps configured in the settings. All are mappable commands, so you can drive them from the keyboard or a macro pad.
* **Reset Location / Rotation / Scale**, **Offset / Rotate / Scale by value**.
* **Cycle Transforms Forward / Backward**: rotate the transforms among the selected actors (with two actors it swaps them), useful to try variants of a composition without moving anything by hand.

### Randomizers
* **Randomize Location / Rotation / Scale** with independent min/max per axis (world or local space, uniform or per-axis scale), using the ranges in the settings or explicit values from Blueprint.
* **Randomize Custom Primitive Data**: assign random values to the configured Custom Primitive Data indices of the selected instanced meshes, for per-instance material variation.

### Arrays
* **Grid**, **Radial**, **Scatter** and **Spline** arrays are created from the selected actor (or the **Source Actors**) and shown as a translucent **ghost preview** you can tune live from the Array tab.
* Post-processing options apply to any array: snap to surface, randomize yaw, orient to a point, scale by distance, rotate around the pivot.
* The spline array places a temporary spline actor you can edit in the viewport; the preview follows it in real time.
* **Confirm** spawns the final actors (individual actors or one Instanced Static Mesh), **Cancel** or **Esc** discards the preview.

### Pivot Actor and Source Actors
* **Set / Select / Clear Pivot Actor**: the first selected actor becomes the pivot used by radial distribution and arrays.
* **Set / Select / Clear Source Actors**: store a selection to use as the template set for arrays and physics tools, independently from what is currently selected.

### Pivot
* **Set Pivot** on selected actors (Center, the 6 faces, the 12 edges and the 8 corners of the bounds) moves the actor pivot without moving the mesh; instances of ISM components are handled too. The same options exist for Static Mesh assets in the Content Browser (see below).

### Renamer
* Rename the selected actors (or the selected assets in the Content Browser) with prefix/suffix, search and replace, numeric suffix stripping, sequential numbering and insert/remove at index, with a **preview** of the result before applying and Undo afterwards.

### Instancing
* **Convert Selected Actors To Instanced Mesh**: group selected static mesh actors by mesh asset and replace them with Instanced Static Mesh actors. Option to keep or delete originals (deleted by default, kept originals are moved to a configurable folder).
* **Explode Selected Instanced Meshes**: the opposite, turn every instance back into an individual actor.

### Landscape to Static Mesh
From the outliner right-click menu on selected landscape proxies:
* **Landscape to Static Mesh (Collision Proxy)**: triangulate each proxy into a static mesh with complex collision and attach an invisible collision proxy under it (used by the physics tools to simulate on terrain).
* **Landscape to Static Mesh (Asset Only)**: create the mesh assets under `/Game/AEU_LandscapeMeshes` without placing them, handy to export terrain to other tools.
* The **Delete Landscape Collision Proxies** Blueprint node removes them again (optionally deleting the assets).

---

## Physics Tools
Native Chaos-based physics tools for set dressing, running directly in the editor world so real level collision is used.

### Physics Drop
* **Physics Drop** (instant): the selected actors (or the Source Actors) fall and settle under physics, the result is baked as their new transforms in one undoable step.
* **Physics Drop (Live)**: watch them fall in the viewport, then **Confirm** to bake the settled transforms or **Cancel** / **Esc** to restore the originals. A maximum duration stops runaway simulations.
* **Selection Simulate Physics / Drop To Ground**, **Set Simulate Physics / Enable Gravity** on the selection are available as Blueprint nodes as well.

### Physics Tools mode
An editor mode (`Physics Tools` in the modes toolbar, also `AEU.PhysicsPaint` in the console) with a Foliage-style panel and a brush painted on the world surface:

| Key | Tool |
|---|---|
| 1 | **Select**: no brush, select actors in the viewport and act on them from the panel (Edit Selected, Paint Selected, Duplicate) |
| 2 | **Paint**: drop simulating copies of the palette meshes under the brush (Shift = Delete) |
| 3 | **Drag**: grab the objects under the brush and move them together, keeping their formation |
| 4 | **Pull**: drag objects toward the brush (Shift = Push) |
| 5 | **Push**: shove objects away from the brush (Shift = Pull) |
| 6 | **Delete**: remove painted objects under the brush |

* **MMB** quick pull, **Shift + MMB** quick push (without leaving the current tool)
* **Alt + LMB drag** or **[ ]** change the active tool's radius, **Ctrl + Alt + LMB drag** changes the spawn count while painting
* **Space** pauses/resumes the simulation, **Enter** confirms, **Esc** cancels
* The **mesh palette** (Level Design settings > Physics Tools > Paint > Mesh Palette) lists the meshes to paint with, each with its own materials, weight, scale range (uniform, free or axis-locked) and an optional *Simulate Physics* flag for objects that must keep simulating after the bake; changes apply live while the mode is open
* **Creation Mode** decides what Confirm bakes: **ISM** (one Instanced Static Mesh component per mesh and material set, lightest), **HISM** (per-instance LOD and culling, good default) or **Actors** (one Static Mesh Actor per object, heavy, for when each object must stay individually editable)
* Every parameter (radius, strength, spawn count, stack on pull, preview settings) lives in the Level Design settings and is edited live from the mode panel

---

## Image Resizer
A dockable tab (toolbar dropdown > Tools > Image Resizer) to batch resize textures without leaving the editor.

* **Work Directory**: pick a Content Browser folder (or use the one currently selected); every texture under it, recursively, is processed. **Individual Assets**: add textures with the asset picker, from the Content Browser selection, by drag-and-drop onto the tab, or with **Open In Image Resizer** in the texture right-click menu.
* The **preview table** shows every texture with its current size and the size it would end up with; dimmed rows are skipped with the current settings, hover a cell to see why.
* **Target Resolution** with presets, and a **Scale Mode**: *Fit* (no side exceeds the target, proportions kept) or *Fill* (the target is covered, one side may exceed it). **Ignore Orientation** reads a 1920x1080 target as 1080x1920 for portrait textures, so a mixed set is limited by long and short side.
* **Allow Downsampling / Upsampling**, **Edge Mode** and **Scaling Filter** (stb_image_resize2 filters).
* **Replace Original(s)**: ON overwrites the source textures (cannot be undone); OFF leaves them untouched and writes resized copies under `/Game/AEU_Resizer/WidthxHeight/` with a configurable **Copy Name Suffix** (`_{W}x{H}` by default, so `T_Foo` becomes `T_Foo_512x512`).
* **Ignore List**: comma-separated name patterns to skip (`atlas,subuv,hdr`).
* A result dialog lists resized, skipped and failed textures and can select the results in the Content Browser.

---

## Folder colors and templates
A **folder template** is a relative path, a colour, and two switches: whether the "Create Folder Structure" dialog creates it, and whether its colour is shared with the team. The plugin ships about 50 of them (`Blueprints`, `Materials/Textures`, `Meshes/StaticMeshes`, `Audio/SFX`, `UI/Widgets`, and so on); the secondary ones are there but unchecked, so you enable the ones your project actually uses. They live in `Editor Preferences > Advanced Editor Utilities > Folder Templates`, with a reset checkbox above the array.

Right-click a folder in the Content Browser to find:

* **Create Folder Structure...**: pick the root folder first, then check what to create in a tree that shows the **final paths** already, each leaf in its own colour. Checking a child checks its parents, unchecking a parent unchecks everything under it.
* **Auto Color Folders (In `<folder>`)**: colours every folder underneath that matches a template. Matching is done on **whole path segments from the end**, so a template `Materials/Textures` colours `/Game/Env/Rocks/Materials/Textures` but never a folder that merely contains the word; when several templates match, the longest match wins. Folders matching nothing are left as they are.

Folder colours are per-user by default (the engine stores them in your `Saved` folder). A template with **Color Shared** on also writes its colour to `Config/AEUFolderColors.ini`, which is versioned: the plugin applies that file at startup, so a colour committed once shows up for everybody on the project without each person recolouring anything.

---

## Content Browser context menus
Every entry and button listed here (and in the next two sections) can be switched off individually in `Editor Preferences > Advanced Editor Utilities > Advanced Settings`, under **Menus & Toolbars** at the bottom of the page: one checkbox per entry. The list is rebuilt at every startup, so updates never leave stale entries behind, and unchecking one takes effect immediately without restarting the editor.

Right-click assets in the Content Browser to find the **Advanced Editor Utilities** section:

| Asset type | Entries |
|---|---|
| Any asset | **Adapt To Naming Convention**, **Select Actors Using This Asset** (selects every actor in the loaded levels that uses the selected assets) |
| Static Mesh | **Copy Sockets**, **Paste Sockets (Replace / Additive)**, **Delete All Sockets**, **Create Multiple Sockets...**, **Set Pivot** (Center, Faces, Edges, Corners: moves the mesh vertices, collision and sockets so the asset pivot changes for every instance) |
| Skeletal Mesh | **Export Sockets to JSON** (Skeleton only / Mesh only / All), **Import Sockets from JSON** (Skeleton only / All), **Delete Sockets** (Skeleton only / Mesh only / All), with live counts |
| Skeleton | **Export Sockets to JSON**, **Import Sockets from JSON...**, **Delete All Sockets** |
| Blueprint | **Reparent Blueprint...**: pick a new parent class for every selected Blueprint in one go |
| Material Instance | **Reparent Material Instance...**: change the parent material and/or the physical material of every selected instance |
| Texture 2D | **Set Texture Settings...** (Texture Group, Compression Settings, sRGB on the whole selection), **Open In Image Resizer**, **Create PBR Textures...**, **Make Seamless...** (both open their own panel; hidden on textures the ignore lists exclude) |
| Anim Sequence | **Change Frame Rate...**: resample the selected animations to another rate keeping their duration, or relabel them when the import got the rate wrong. Optionally converts a copy and leaves the original alone |
| Data Table | **Sync With Data Assets**, **Push To Data Assets** (see below) |
| Data Asset | **Convert To Data Table...** (see below) |
| User Defined Struct | **Create Data Table...**: an empty table using the struct as row type; a dialog lets you pick the folder and the name (defaults to the struct's folder and `DT_<StructName>`) |

---

## Data Table / Data Asset conversion
Data Tables are great to edit, sort and export as CSV; Data Assets are great to reference from other assets. These tools keep both, with the table and its assets paired by name:

```
<Folder>/DT_Enemies              the table
<Folder>/DA_Enemies/DA_<Row>     one Data Asset per row
```

Prefixes come from your Naming Convention (`DT_`, `DA_`, `F_` by default). A Data Asset class is **compatible** with a row struct when it either has a single property of that exact struct type (the recommended layout, generated automatically if you let the tool create the class) or one property per row member with the same name and type; partial matches are refused so no column is ever silently dropped.

### From a Data Table
* **Sync With Data Assets** (also the **Sync Data Assets** button in the Data Table editor toolbar, both shown once the `DA_` folder exists): existing Data Assets are the source of truth. Every asset in the `DA_` folder is read back into its row (the row is created if missing), and every row without an asset gets one created from the row. Nothing is deleted on either side and an existing asset is never overwritten from the table.
* **Push To Data Assets** (also in the toolbar): the opposite direction, for when the work was done in the table. Every row is written to its asset, overwriting existing ones and creating the missing ones; nothing is deleted.
* When Data Assets have to be created and the folder holds none yet, a dialog lists the compatible classes found in the project (native and Blueprint) and offers **Create New Class**, which generates a Blueprint of `PrimaryDataAsset` (default name `DA_<Base>_Class`) with a single `Data` variable of the row struct type.

### From Data Assets
* **Convert To Data Table...** on one or more Data Assets of the same class:
  * assets already in a `DA_<X>` folder: the table is `DT_<X>` in the parent folder (updated if it exists, created otherwise) and every same-class asset of the folder becomes a row; nothing is moved
  * assets in a plain folder `<F>`: the table `DT_<F>` is created in that folder and the selected assets are moved into `<F>/DA_<F>/`
  * when no table exists, a dialog lists the compatible row structs or offers **Create New Struct**, which generates a User Defined Struct (default `F_<X>`) mirroring the editable properties of the class
* **Sync Data Table** button in the Data Asset editor toolbar, shown only when the paired `DT_` exists in the parent folder: writes that asset into its row.

### Changing the schema
With the single-struct layout the struct is the only schema: edit it, save, and both the table rows and the Data Asset instances follow (existing members keep their values, new ones take the default). Then fill the new values where you prefer and run **Sync** (if you edited the assets) or **Push** (if you edited the table). With a class that mirrors the struct member by member, the two schemas are independent and must be kept in sync by hand.

---

## Asset editor toolbar buttons
* **Capture Nodes** in every asset editor that has a node graph
* **Sync Data Assets** and **Push To Data Assets** in the Data Table editor
* **Sync Data Table** and **Open Data Table** in the Data Asset editor (when the paired table exists)
* **Open Data Table** in the User Defined Struct editor (when at least one table uses the struct as row type; with several, one click opens them all)
* **Check All / Uncheck Unchanged** in the Material Instance editor: the same one-click override toggle as the Material Parameters panel, on the instance you have open
* **Export...** in the Static Mesh editor (after the Reimport buttons) and in the Texture editor (next to Compress and Reimport): the same action as `Asset Actions > Export...`, with the format picker, without going back to the Content Browser for it
* **Show Pivot**, **Bounds**, **Simple Collision** and **Complex Collision** in the Static Mesh editor: the Show menu toggles worth having one click away while inspecting a mesh, each with its own switch. They keep their shortcuts and stay in step with the Show menu (this group applies when the asset is reopened)

---

## Mesh Socket Utilities

A Blueprint Function Library (`UAEU_BlueprintFunctionLibrary`) for batch socket operations on Static Meshes, Skeletal Meshes, and Skeletons. Also accessible via **right-click context menus** in the Content Browser on compatible asset types.

### Static Mesh Sockets
* **CopySocketsFromStaticMesh**: copy all sockets from a source to one or more target static meshes.
* **DeleteAllSocketsFromStaticMesh**: remove all sockets from a static mesh.
* **CreateMultipleStaticMeshSockets**: batch-create numbered sockets with cumulative location/rotation offset.
* **ExportStaticMeshSocketsToJSON** / **ImportStaticMeshSocketsFromJSON**: export/import sockets to/from JSON files (default filename: `{MeshName}_sockets.json`).

### Skeletal Mesh Sockets
* **CopySocketsFromSkeletalMesh**: copy sockets between skeletal meshes. Uses the **Bone Name Resolver** (see below) to automatically remap bones across different skeleton standards.
* **DeleteAllSocketsFromSkeletalMesh**: remove all mesh-local sockets from a skeletal mesh.
* **CreateSocketsOnMatchingBones**: create sockets on all bones matching a wildcard pattern (e.g. `*finger*`, `hand_*`).
* **ExportSkeletalMeshSocketsToJSON** / **ImportSkeletalMeshSocketsFromJSON**: export/import sockets to/from JSON. Exports include skeleton-inherited sockets. Import uses the Bone Name Resolver for cross-skeleton compatibility.

### Skeleton Sockets
* **CopySocketsFromSkeleton**: copy sockets between skeletons with automatic bone name resolution.
* **DeleteAllSocketsFromSkeleton**: remove all sockets from a skeleton.
* **ExportSkeletonSocketsToJSON** / **ImportSkeletonSocketsFromJSON**: export/import skeleton sockets to/from JSON with bone name resolution on import.

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
1. **Exact match**: bone name exists on the target as-is.
2. **Prefix stripping**: removes known prefixes (`mixamorig:`, `mixamorig_`, `Bip01_`, `Genesis8_`, etc.) and retries exact match.
3. **Mapping table lookup**: looks up the bone in the mapping table (51 bone groups covering the full body and all fingers). Once the target skeleton's standard is detected, it is cached and prioritized for all subsequent lookups.
4. **Levenshtein fuzzy match**: normalized string similarity (default threshold: 0.8) against all target bones, with prefix stripping applied.
5. **Skip with warning**: if nothing matches, the socket is skipped and a warning is logged.

### Standard Detection Caching
On the first bone lookup, the resolver scans both source and target skeletons to detect which standard they use (by counting bone name matches). The detected standards are **cached for the entire operation**, so subsequent bones skip directly to the right mapping, no need to cycle through all standards every time.

### Customization
* **Custom mapping file**: call `SetBoneMappingFile()` from Blueprint or C++ to load a custom JSON mapping table instead of the default one.
* **Fuzzy match threshold**: adjust `FuzzyMatchThreshold` (0.0–1.0, default 0.8) to make fuzzy matching more or less strict.
* **Mapping JSON location**: default: `{PluginDir}/Config/BoneMapping.json`. Editable to add new skeleton standards or bone groups.

---

## Blueprint and Remote Control functions
Everything above is also exposed to Editor Utility Widgets and Blueprints (`UAEU_BlueprintFunctionLibrary`, `UAEU_LevelDesignLibrary`), all marked *Development Only*. A few nodes worth knowing about:
* **Run Map Check**: runs `Build > Map Check` and returns the error and warning counts, so a validation widget or an automation script can fail on map problems.
* **Start / Stop / Toggle PIE**, **Is Play In Editor Running**, **Toggle Viewport Realtime**.
* **Open Settings** (any Project Settings or Editor Preferences section by name), **Open AEU Utility**, **Open World Locker**, **Open Image Resizer**, **Focus In Content Browser**, **Show Selection In Explorer**.
* **Update Redirector References In Selection**: fix up and remove the redirectors of the selection (or of `/Game`).
* **Select Actors Using Assets / Same Meshes / Same Materials**, **Organize World Outliner**, **Delete Null Static Mesh Actors**, **Reimport Data Table**.

`UAEU_RemoteControlLibrary` exposes the most useful actions to the **Remote Control** plugin with string parameters and choice lists, so they can be bound to a web panel or a stream deck: apply a view mode, execute a configured command, align / distribute / snap / move / rotate / scale the selection, swap transforms, adapt the selected assets to the naming convention.
