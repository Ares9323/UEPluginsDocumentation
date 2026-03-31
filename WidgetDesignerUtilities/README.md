# Widget Designer Utilities

Adds color-coding, batch rename, binding warnings and widget extraction tools to the UMG Widget Designer hierarchy, making it easier to visually identify and organize widgets in complex UI layouts.

Available on [FAB](https://www.fab.com/listings/f2c89fbf-cf4e-4cac-99b5-709f29920d2d)

## How to activate on a single project
* Open plugins
* Look for Widget Designer Utilities
* Activate the checkbox
* Restart the editor

## How to activate globally
* Open the Unreal Engine installation folder (e.g., `C:\Program Files\Epic Games\UE_5.5\Engine\Plugins\Marketplace\WidgetDesignerUtilities`)
* Open the `WidgetDesignerUtilities.uplugin` file in a text editor
* Change the `EnabledByDefault` property to `true`
* Change the `Installed` property to `false` to avoid showing the plugin in the project plugins list

## The Problem

The UMG Widget Designer hierarchy can become extremely difficult to navigate in complex UI layouts. With dozens of nested VerticalBoxes, HorizontalBoxes, and Buttons, it's nearly impossible to visually distinguish one section from another. All widgets look the same in the tree, making it hard to find what you're looking for. Additionally, there's no built-in way to batch rename widgets, detect performance-costly property bindings at a glance, or quickly extract a group of widgets into a reusable Widget Blueprint.

## The Solution

Widget Designer Utilities adds a lightweight context menu (activated via **Middle-Click** or a configurable key) directly in the UMG hierarchy, providing color-coding, batch operations, and extraction tools — all without modifying the engine.

## Features

### Hierarchy Color-Coding

Assign colors to widgets in the hierarchy to visually group and identify sections of your UI.

- **Quick color presets** — Middle-click on any widget and choose from configurable preset colors in a single click
- **Custom colors** — Open a full color picker for any color you need
- **Background and/or text coloring** — Choose between background tint, text color, or both (configurable in settings)
- **Adjustable opacity** — Control the background tint intensity with a slider
- **Multi-selection support** — Apply colors to multiple selected widgets at once
- **Per-asset storage** — Colors are saved inside the Widget Blueprint `.uasset` file via a Blueprint Extension, no external files needed
- **Automatic orphan cleanup** — Colors assigned to deleted or renamed widgets are automatically purged
- **Rename-resilient** — Colors are stored by internal FName, which survives display name changes. Single-widget renames are auto-detected and the color transfers to the new name
- **Clear Color / Clear All Colors** — Remove colors from selection or from the entire blueprint

### Binding Performance Warnings

Automatically highlights widgets that have property bindings, which tick every frame and can be a significant performance concern.

- **Icon tinting** — The widget type icon turns orange for widgets with active property bindings
- **Detailed tooltip** — Hover over the tinted icon to see exactly which properties have bindings and how many
- **Configurable** — Enable/disable and customize the warning color in settings
- **Zero setup** — Works automatically on every Widget Blueprint you open

### Batch Rename (Search/Replace)

Rename multiple widgets at once with find-and-replace, directly from the hierarchy context menu.

- **Search and Replace** — Find text in widget names and replace it across all selected widgets
- **Strip numeric suffix** — Automatically removes `_1`, `_2`, etc. suffixes (enabled by default) — perfect after duplicating widgets
- **Actual variable rename** — Uses the engine's `RenameWidget` API, so all Blueprint references are updated correctly
- **Rename validation** — Invalid renames are skipped with a warning, never crashes
- **Undo support** — Each rename operation is a full editor transaction

### Extract to Widget Blueprint

Select a group of widgets and extract them into a new, reusable Widget Blueprint with a single click.

- **One-click extraction** — Select widgets with the same parent, click "Extract to Widget Blueprint...", choose a name and location
- **Parent class picker** — Choose the parent class for the new Widget Blueprint (UUserWidget or any custom subclass)
- **Deep copy** — Uses the engine's copy/paste API for a proper deep copy with no broken references
- **Same-parent validation** — The option only appears when all selected widgets share the same parent, preventing invalid extractions
- **Clipboard preservation** — Your clipboard content is saved and restored after the operation

### Settings

All features are configurable via **Editor Preferences > Plugins > Widget Designer Utilities**.

#### Input
| Setting | Default | Description |
|---------|---------|-------------|
| Context Menu Button | Middle Mouse Button | Mouse button to open the WDU context menu |
| Context Menu Key | F1 | Keyboard key to open the WDU context menu |
| Require Ctrl | false | Require Ctrl modifier |
| Require Shift | false | Require Shift modifier |
| Require Alt | false | Require Alt modifier |

#### Appearance
| Setting | Default | Description |
|---------|---------|-------------|
| Apply Text Color | false | Color the text of hierarchy rows |
| Apply Background Color | true | Apply a background tint to hierarchy rows |
| Background Alpha | 0.5 | Opacity of the background tint (0-1) |

#### Binding Warnings
| Setting | Default | Description |
|---------|---------|-------------|
| Highlight Bindings | true | Tint widget icons for widgets with property bindings |
| Binding Warning Color | Orange | Color used for the binding warning |

#### Color Presets
Customizable array of preset colors shown in the quick-select submenu. Default: Red, Orange, Yellow, Green, Cyan, Blue, Purple, Pink.

A **Hierarchy Preview** widget in the settings page shows a live preview of how your color settings will look in the actual hierarchy.

## Context Menu Reference

The context menu appears when you **Middle-Click** (or press **F1**) on a widget in the hierarchy:

```
-- HIERARCHY COLOR --
  Set Color          >  [Color presets + Custom Color...]
  Clear Color            (only if widget has a color)
  Clear All Colors       (only if any colors exist)

-- EXTRACT --
  Extract to Widget Blueprint...  (only if all selected share same parent)

-- RENAME --
  Batch Rename (Search/Replace)...

-- SETTINGS --
  Plugin Settings...     (opens Editor Preferences)
```

## Technical Details

- **Editor-only** — Zero runtime overhead, does not ship with packaged builds
- **Non-destructive** — Color data is stored in a `UBlueprintExtension` inside the Widget Blueprint; removing the plugin leaves no trace
- **Periodic refresh** — Colors are re-applied every 0.5 seconds to handle tree rebuilds from expand/collapse
- **Slate traversal** — Finds hierarchy widgets by traversing the Slate widget tree, same pattern used by engine editor plugins
- **Cross-editor support** — Works with multiple Widget Blueprint editors open simultaneously
