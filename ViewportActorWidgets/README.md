![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/ViewportActorWidgets/Images/Logo.png)

# Viewport Actor Widgets

Pin interactive UMG widgets to your actors directly in the editor viewport. Build per-actor property panels, action buttons that call functions on the selected actor, live status displays, and custom editor tools — all using UMG, no Slate or editor-module C++ required.

Coming soon on [FAB](https://www.fab.com/listings/bdcc831b-28ce-47b0-8b23-79941a080c2d)

## How to activate on a single project
* Open the Plugins window
* Search for "Viewport Actor Widgets"
* Activate the checkbox
* Restart the editor

## How to activate globally
* Open the Unreal Engine installation folder (e.g., `C:\Program Files\Epic Games\UE_5.5\Engine\Plugins\Marketplace\ViewportActorWidgets`)
* Open the `ViewportActorWidgets.uplugin` file in a text editor
* Change the `EnabledByDefault` property to `true`
* Change the `Installed` property to `false` to avoid showing the plugin in the project plugins list

## The Problem

Authoring custom editor UI for an actor normally means writing a Slate widget, an Editor module, a property type customization, or a full Editor Utility Widget. None of these scale well when you just want a couple of action buttons above a level actor, or a contextual DetailsView panel that follows the selected actor, or a tiny status HUD pinned to a procedural prop. UMG would be the natural tool — but UMG widgets aren't designed to live in the editor viewport attached to an arbitrary actor.

## The Solution

Viewport Actor Widgets adds a single component you drop on any actor. Assign your UMG widget class, choose a render mode (Worldspace 3D quad or Screen Overlay), and the widget appears pinned to the actor's transform in the editor viewport — fully interactive, no Slate code required.

## Getting Started

1. Add a **ViewportActorWidgetComponent** to the actor you want to attach a widget to.
2. Set its **Widget Class** to a UMG widget. If you want the widget to know about its host actor, derive the widget from **ViewportActorWidget** instead of UUserWidget so you get the `OwnerActor` / `OwnerComponent` references populated before construction.
3. Pick a **Render Mode**:
   - **Worldspace 3D** — the widget is rendered as a textured quad in the world. To see it and interact with it, activate the **Viewport Actor Widgets** editor mode from the toolbar.
   - **Screen Overlay** — the widget appears in screen space above the actor when the actor is selected. No editor mode needed.
4. (Optional) Tweak **Draw Size**, **Auto Size**, **Screen Alignment** and **Screen Anchor Offset** to fine-tune the position and size.

## Features

### Two Render Modes

#### Worldspace 3D

The widget is rendered as a textured quad in the world via a transient `UWidgetComponent`, scaling and rotating with the actor's transform.

- **Fully interactive** — Click, hover, mouse-leave and mouse-wheel events are raycast into the offscreen Slate window. Buttons, sliders, scroll boxes, list views, and even DetailsView panels respond as expected.
- **Camera-zoom safe scrolling** — Wheel events that reach the scroll limit of a ScrollBox are consumed so they don't bubble up to the editor viewport's camera zoom.
- **DPI-aware** — Works correctly on 4K / high-DPI displays at any Windows scaling factor.
- **Construction Script survival** — A transient shadow actor pattern keeps the widget alive across SCS rerun, so editing your actor BP doesn't kill the live widget.

#### Screen Overlay

The widget lives in the editor's Slate hierarchy, projected to screen-space above the actor.

- **Auto-show on selection** — The overlay appears when its owning actor is selected and tears down on deselect.
- **Full popup-picker compatibility** — Color picker, asset picker, class picker, struct viewer all work natively (they live in the editor's regular Slate window hierarchy).
- **Configurable anchoring** — `ScreenAlignment` (pivot) and `ScreenAnchorOffset` let you place the widget exactly where you want it relative to the actor's projected position.

### Owner-Bound Widgets

Derive your widget from **ViewportActorWidget** instead of UUserWidget to get:

- `OwnerActor` — the AActor that hosts the component
- `OwnerComponent` — the ViewportActorWidgetComponent itself
- `OnOwnerActorSet` — fired after the references are populated, before Construct

The owner references are set **before** `Initialize` / `PreConstruct` / `Construct` run, so you can safely call `DetailsView->SetObject(OwnerActor)` in PreConstruct without the usual null-binding workaround.

### Editor Mode

The Worldspace 3D path is gated by an editor mode (`EM_ViewportActorWidgets`). Activate it from the toolbar's editor modes dropdown to see and interact with 3D widgets in the level. The mode is auto-entered when you select an actor that has a Worldspace3D ViewportActorWidgetComponent.

### Blueprint Library

`UViewportActorWidgetsLibrary::GetOwningActor(Widget)` performs a reverse lookup from any UUserWidget back to the actor that owns its host component — useful when widget BPs are reused across multiple actors.

### Settings

All configuration is exposed via **Editor Preferences > Plugins > Viewport Actor Widgets** (per-user project settings).

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Overlay System | true | Master switch for the Screen Overlay path |

## Technical Details

- **Editor-only** — The whole plugin is editor-targeted. Zero runtime overhead, does not ship with packaged builds.
- **Transient shadow actors** — Worldspace3D rendering uses RF_Transient actors that are not saved to the map; they're decoupled from SCS and survive Construction Script rerun by re-resolving the descriptor by name each tick.
- **TRASH_ filtering** — After SCS rerun the old component instance gets renamed to `TRASH_*` until GC. The subsystem filters these to avoid spawning duplicate shadows.
- **Input routing** — Click / move / wheel events are routed via `FSlateApplication::RoutePointerDownEvent`, `RoutePointerMoveEvent` and `RoutePointerUpEvent` against the offscreen window's widget path resolved by `LocateWidgetInWindow`.
- **Wheel handling** — Mouse wheel uses a manual leaf-to-root bubble through the resolved widget path; the editor's standard `ProcessMouseWheelOrGestureEvent` expects screen-global coords and isn't viable for offscreen windows.

## Limitations

- **Worldspace 3D cannot host engine pop-up pickers** (color picker, asset picker, class picker, struct viewer). These are managed by `FMenuStack` and have built-in "outside click dismisses" detection; our virtual click coords live in the offscreen window, not in screen space, so the popup is dismissed immediately after opening. **Workaround: use ScreenOverlay mode for widgets that rely on those pickers** — overlay clicks are real screen-space clicks and everything works natively.
- **Editor-only.** The plugin is targeted at editor tooling and is not packaged in shipping builds.

## Tips

- **Mark BP variables as Instance Editable** if you want DetailsView UMG widgets to actually commit edits back to the actor. Without Instance Editable the property is read-only at the instance level and the DetailsView UI appears greyed-out.
- For DetailsView UMG hosted by VAW, call `SetObject(OwnerActor)` in **PreConstruct** (not Construct) — this guarantees the binding is in place before the panel renders for the first time.
- If you need to refresh a DetailsView's filter (`CategoriesToShow` / property whitelist) at runtime, call `SetObject(nullptr)` and then `SetObject(OwnerActor)` again to force a rebuild.
