![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/Logo.png)

# AresGraphManager

A visual enhancement plugin for Unreal Engine graph editors. Replaces default spline wires with clean 45-degree angled connections, adds auto-connect features, node bypass, graph cleanup tools, and a customizable editor theme.

> ⚠️ **Note:** This plugin is currently in an experimental stage and is under active development. If you encounter any issues or have suggestions, **please reach out before leaving a negative review** — your feedback helps me improve the product and I'm happy to assist with any problems directly. You can contact me through the [support page](https://github.com/Ares9323/UEPluginsDocumentation/issues) or the [Epic Developer Community](https://dev.epicgames.com/community/profile/k7ba/Ares9323).

Available on [FAB](https://www.fab.com/portal/listings/e7d9e12b-dcc0-426e-b409-718df206ac2a)

---

## Installation

1. Install the plugin from FAB
2. Open **Edit > Plugins**
3. Search for **AresGraphManager**
4. Enable the checkbox
5. Restart the editor

## Settings

All settings are in **Edit > Project Settings > Plugins > AresGraphManager**. Settings are saved globally (shared across all projects).

---

## Features

### Angled Wire Style

![AresGraphManager](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/RandomNodes.png)

AresGraphManager replaces the default curved splines with clean angled wires using 45-degree diagonals. Wires automatically choose between horizontal-dominant (single diagonal) and vertical-dominant (diagonal + vertical + diagonal) layouts based on pin positions.

Backward connections (when the output pin is to the right of the input pin) use S-shaped or U-turn routing to keep the graph readable.

![Backward Nodes](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/BackwardNodes.png)

| Setting | Default | Description |
|---------|---------|-------------|
| Wire Style | AresGraphManager | `AresGraphManager` for angled wires, `Default` for standard splines |
| Wire Alignment | Right | Horizontal segment alignment preference |
| Wire Priority | None | Alignment priority (`None`, `Node`, `Pin`) |
| Wire Thickness | 0.5 | Wire thickness multiplier (0.0 - 1.0) |
| Horizontal Offset | 5 | Horizontal distance from node before wire starts turning |
| Incremental Offset | 5 | Additional offset per pin to prevent overlapping vertical segments |
| Backward S Down Offset | 20.0 | Midpoint vertical shift for downward S-wires |
| Backward S Up Offset | 0.0 | Midpoint vertical shift for upward S-wires |
| Debug | false | Show debug visualization on wires |

![Alignment](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/AlignLeftRight.gif)

![Horizontal Offset](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/HorizontalOffset.gif)

![Incremental Offset](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/IncrementalOffset.gif)

### Supported Graphs

![Custom Graph Support](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/CustomGraphSupport.gif)

![Behavior Tree](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/BehaviorTree.png)

AresGraphManager works on multiple graph types, each toggleable individually:

- **Blueprint Graph** — All Blueprint graph types
- **Material Graph** — Material editor graphs (with correct wire colors through reroute nodes)
- **Animation Graph** — AnimGraph, State Machines, Transitions
- **Niagara Graph** — Particle system graphs
- **Behavior Tree Graph** — AI behavior tree editor (vertical wire routing)
- **Control Rig Graph** — Animation rigging graphs
- **Reference Viewer Graph** — Asset reference graphs
- **Custom Schemas** — Add any graph editor via class path in settings

### Wire Color Through Reroute Nodes

![Reroute Color](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/RespectMaterialPinColors.gif)

AresGraphManager propagates wire colors correctly through reroute/knot node chains. In the default engine, wires lose their color after a reroute node and become grey. AresGraphManager traces back to the original source pin and preserves the correct color. This works across all graph types.

---

### Auto Connect & Insert

![Auto Connect](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/AutoConnect.gif)
![Auto Insert](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/AutoInsert.gif)

Drag a node near other nodes and compatible pins are automatically connected when you release. These features are reimplemented natively in AresGraphManager to work correctly with custom wire styles.

When the modifier is set to `None`, holding any modifier key (Alt, Ctrl, Shift) temporarily disables the feature, allowing you to drag freely without triggering auto-connect or insert. Holding the modifier also re-enables node-avoidance on the dragged node, so surrounding wires reshape around it.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Auto Connect | true | Toggle auto-connect on drag release |
| Auto Connect Modifier | None | Modifier key required (`None`, `Alt`, `Ctrl`, `Shift`) |
| Auto Connect Radius | 50 | Detection radius for compatible pins (50 - 500) |
| Enable Insert Node On Wire | true | Drop a node on an existing wire to insert it inline |
| Insert Node Modifier | None | Modifier key required for insert (`None`, `Alt`, `Ctrl`, `Shift`) |
| Override New Wire Preview Color | false | Override the preview color for new connections |
| New Wire Preview Color | Green | Color for new connection preview wires |
| Override Deleted Wire Preview Color | true | Override the preview color for wires being removed |
| Deleted Wire Preview Color | Red | Color for wires that will be removed during insert |

**How it works:**

1. Start dragging a node
2. Move it near compatible pins on other nodes
3. A preview wire appears showing the potential connection
4. Release to confirm

**Insert Node on Wire:**

![Insert on Wire](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/InsertOnWire.gif)

1. Start dragging a node
2. Move it over an existing wire
3. The wire highlights and preview connections appear
4. Release to insert the node into the wire (old wire is broken, two new connections are created)

While auto-insert is potentially active (no modifier held), surrounding wires keep their natural path so you can see exactly where the node will land. Holding the insert-suppress modifier (Alt by default with `Insert Node Modifier = None`) disables insert detection and lets node-avoidance reshape neighbouring wires around the dragged node.

---

### Bypass Node

Remove a node from the execution flow while keeping the chain intact. The upstream and downstream nodes are reconnected automatically. The bypass key is ignored while typing in text fields (node comments, rename, search boxes).

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Bypass Node | false | Enable the bypass feature |
| Bypass Node Key | X | Key to trigger bypass |
| Copy Bypassed Nodes To Clipboard | false | Copy nodes to clipboard before removing them |

**Shortcuts:**

| Action | Shortcut | Description |
|--------|----------|-------------|
| Bypass node | `X` (while dragging) | Reconnects upstream to downstream and removes the node |
| Delete & Bypass | `Alt + X` (no drag needed) | Bypasses selected nodes and deletes them |
| Delete node | `X` (already disconnected) | Deletes the node entirely |

![Bypass](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/Drag+X.gif)

![Bypass Selected](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/X.gif)

![Detach](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/Alt+X.gif)

---

### Node Commands

Keyboard commands for everyday node editing. Each one has its own enable switch and key in the **Node Commands** category of the Shortcuts settings, is one undo step, and is ignored while you type in a text field.

| Command | Default | What it does |
|---------|---------|--------------|
| Creation menu from pin | `Tab` | Opens the node creation menu filtered on the pin under the mouse, as if you had dragged a wire from it, and connects the new node. Without a pin under the mouse it uses the selected node's first free output. Works in every graph editor. |
| Replace node | `Ctrl + H` | Opens the creation menu already filtered for the selected node's main pin. The node you pick takes the old node's place and keeps every link that fits. Cancel the menu and nothing changes. Blueprint and Material graphs. Runs on release, so `Ctrl + H` + click spawn shortcuts keep working. |
| Rename member | `F2` | With a node that refers to a variable, function, custom event or macro of this Blueprint selected, renames that member the same way My Blueprint does, updating every reference. On any other node `F2` is the engine's own rename. |
| Edit node comment | `Shift + F2` | Opens the node's comment bubble with the cursor in its text. |
| Duplicate variable per link | `Ctrl + Shift + V` | For a getter (or another pure node with one output) wired into several pins, makes one copy per link, each placed next to the pin it feeds and aligned on it. Works across macros, Select/Switch and reroutes; a link that cannot be moved stays on the original. |

> **Key remappers**: tools that remap Shift + F-keys system-wide (for example PowerToys Keyboard Manager turning Shift + F1…F12 into F13…F24) stop `Shift + F2` from reaching the editor. Exclude the editor from the remap or pick another key in the settings.

---

### Graph Cleanup

![Cleanup](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/CleanupDisconnectedWires.gif)

Remove orphaned reroute nodes and broken pin links from the current graph with a single shortcut. A modifier key is always required to avoid conflicts with the Delete key.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Graph Cleanup | true | Toggle the cleanup feature |
| Graph Cleanup Key | Delete | Key to trigger cleanup |
| Graph Cleanup Modifier | Alt | Modifier key required (`Alt`, `Ctrl`, `Shift` — no `None` option) |

**Shortcut:** `Alt + Delete`

**What it removes:**

- **Orphaned reroute nodes** — reroute/knot nodes where following the chain in either direction never reaches a real node. Chains of reroutes that connect two real nodes are preserved.
- **Broken pin links** — null pointer references in pin connections

---

### Editor Theme

![Editor Theme](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/EditorTheme.gif)

Customize the overall editor appearance with luminosity, saturation, and hue adjustments. Color transformations use the perceptually uniform LAB color space for accurate results. Background and accent colors can be tuned independently so you can keep a neutral chrome and still get vivid highlights (or vice-versa).

Editor preferences are never persisted to disk by the plugin — the grid colors you see while AresGraphManager is enabled are computed in-memory each session, so disabling or uninstalling the plugin restores your original UE preferences automatically.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Theme | true | Toggle the editor theme |
| Theme Luminosity | 0 | Brightness adjustment for background/panel/neutral chrome (-100 to +100) |
| Theme Saturation | 0 | Color intensity for background/panel/neutral chrome (-100 to +100) |
| Accent Saturation | 0 | Desaturation for accent colors only — Primary, Highlight, Select, Notifications (-100 to 0). UE accents are fully saturated by default so only desaturation has an effect. |
| Accent Luminosity | 0 | Brightness adjustment for accent colors only (-100 to +100), independent of Theme Luminosity |
| Theme Hue | 210 | Hue shift (0 - 360 degrees) |
| Keep Foreground Luminosity | false | Prevent text luminosity from shifting |

---

### Node Theme

![Node Theme](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AresGraphManager/Images/NodeTheme.gif)

Customize the appearance of graph nodes. Changing `Enable Node Theme` requires an editor restart.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Node Theme | true | Toggle node appearance customization (requires restart) |
| Regular Node Opacity | 0.75 | Regular node background opacity (0.0 - 1.0) |
| Var Node Opacity | 0.5 | Variable node background opacity (0.0 - 1.0) |
| Node Header Opacity | 0.25 | Header color overlay opacity (0.0 - 1.0) |
| Node Header Saturation | 1.0 | Header color saturation (0.0 - 1.0) |

---

### Compatibility

AresGraphManager is **not compatible** with other graph-enhancement plugins that override wire drawing or auto-connect behavior. Known overlapping plugins:

- [Node Graph Assistant](https://www.fab.com/listings/525a33bb-9b05-405d-bf3e-42ca990fb31b)
- Electronic Nodes
- Gridline Blueprints

If one of these is installed, AresGraphManager logs a warning at editor startup. Disable one of the two to avoid feature overlap on Auto Connect, Auto Insert, Wire Style, and connection drawing. AresGraphManager does not modify any other plugin's configuration files.

---

### Reset

Each settings category has a dedicated reset toggle in the **Reset** section. Check the box to restore defaults for that category:

- Reset Wire Style
- Reset Theme
- Reset Node Theme
- Reset Auto Connect & Insert
- Reset Bypass
- Reset Cleanup

---

## Shortcut Reference

| Shortcut | Requires | Action |
|----------|----------|--------|
| `X` while dragging | Bypass enabled | Bypass dragged node (reconnect flow and remove) |
| `Alt + X` | Bypass enabled | Delete & bypass selected nodes |
| `X` on disconnected node | Bypass enabled | Delete disconnected node |
| `Alt + Delete` | Cleanup enabled | Clean up orphaned reroutes and broken links |
| `Tab` | Node Commands | Creation menu filtered on the pin under the mouse |
| `Ctrl + H` | Node Commands | Replace the selected node, keeping its links |
| `F2` | Node Commands | Rename the variable / function / event / macro the node refers to |
| `Shift + F2` | Node Commands | Edit the node comment bubble |
| `Ctrl + Shift + V` | Node Commands | One getter copy per link |
| Hold any modifier while dragging | Auto Connect/Insert set to None | Temporarily disable auto-connect/insert and enable node-avoidance on the dragged node |

*All keys and modifiers are configurable in settings. Bypass keys are ignored while typing in text fields.*

---

## FAQ

**Does this modify engine files?**
No. AresGraphManager hooks into the editor's connection drawing pipeline at runtime. No engine source changes required.

**Does this modify my editor preferences?**
No. The plugin computes its theme colors in-memory each session and never calls `SaveConfig()` on `UEditorStyleSettings`. Your original Editor Preferences ini stays untouched, so disabling or uninstalling AresGraphManager restores the default UE look automatically.

**Can I use this with other graph editor plugins?**
AresGraphManager is not compatible with NGA, Electronic Nodes or Gridline Blueprints — their wire drawing and auto-connect features overlap with ours. Disable one of the two to avoid conflicts.

**Can I disable just the theme and keep the wires?**
Yes. Every feature category (wires, theme, node styling, auto-connect, bypass, cleanup) can be toggled independently.

**Does this affect packaged games?**
No. AresGraphManager is editor-only and is not included in packaged builds.

**Can I switch back to default wires?**
Yes. Set `Wire Style` to `Default` in settings, or disable AresGraphManager entirely with the `Enable AresGraphManager` toggle.

**Why does changing Enable Node Theme require a restart?**
The node theme modifies Slate style brushes at startup. Disabling it at runtime doesn't restore the original brushes, so a restart is needed to apply the change cleanly.

**Can I temporarily disable auto-connect while dragging?**
Yes. When the modifier is set to `None`, holding any modifier key (Alt, Ctrl, Shift) temporarily suppresses auto-connect and insert-node. Surrounding wires will then reshape around the dragged node via node-avoidance.
