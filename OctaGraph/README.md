![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/Logo.png)

# OctaGraph

A visual enhancement plugin for Unreal Engine graph editors. Replaces default spline wires with clean 45-degree angled connections, adds auto-connect features, node bypass, graph cleanup tools, and a customizable editor theme.

Available on [FAB](https://www.fab.com/sellers/Ares9323)

---

## Installation

1. Install the plugin from FAB
2. Open **Edit > Plugins**
3. Search for **OctaGraph**
4. Enable the checkbox
5. Restart the editor

## Settings

All settings are in **Edit > Project Settings > Plugins > OctaGraph**. Settings are saved globally (shared across all projects).

---

## Features

### Angled Wire Style

![OctaGraph](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/RandomNodes.png)

OctaGraph replaces the default curved splines with clean angled wires using 45-degree diagonals. Wires automatically choose between horizontal-dominant (single diagonal) and vertical-dominant (diagonal + vertical + diagonal) layouts based on pin positions.

Backward connections (when the output pin is to the right of the input pin) use S-shaped or U-turn routing to keep the graph readable.

![Backward Nodes](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/BackwardNodes.png)

| Setting | Default | Description |
|---------|---------|-------------|
| Wire Style | OctaGraph | `OctaGraph` for angled wires, `Default` for standard splines |
| Wire Alignment | Right | Horizontal segment alignment preference |
| Wire Priority | None | Alignment priority (`None`, `Node`, `Pin`) |
| Wire Thickness | 0.5 | Wire thickness multiplier (0.0 - 1.0) |
| Horizontal Offset | 5 | Horizontal distance from node before wire starts turning |
| Incremental Offset | 5 | Additional offset per pin to prevent overlapping vertical segments |
| Backward S Down Offset | 20.0 | Midpoint vertical shift for downward S-wires |
| Backward S Up Offset | 0.0 | Midpoint vertical shift for upward S-wires |
| Debug | false | Show debug visualization on wires |

![Alignment](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/AlignLeftRight.gif)

![Horizontal Offset](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/HorizontalOffset.gif)

![Incremental Offset](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/IncrementalOffset.gif)

### Supported Graphs

![Custom Graph Support](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/CustomGraphSupport.gif)

![Behavior Tree](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/BehaviorTree.png)

OctaGraph works on multiple graph types, each toggleable individually:

- **Blueprint Graph** — All Blueprint graph types
- **Material Graph** — Material editor graphs (with correct wire colors through reroute nodes)
- **Animation Graph** — AnimGraph, State Machines, Transitions
- **Niagara Graph** — Particle system graphs
- **Behavior Tree Graph** — AI behavior tree editor (vertical wire routing)
- **Control Rig Graph** — Animation rigging graphs
- **Reference Viewer Graph** — Asset reference graphs
- **Custom Schemas** — Add any graph editor via class path in settings

### Wire Color Through Reroute Nodes

![Reroute Color](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/RespectMaterialPinColors.gif)

OctaGraph propagates wire colors correctly through reroute/knot node chains. In the default engine, wires lose their color after a reroute node and become grey. OctaGraph traces back to the original source pin and preserves the correct color. This works across all graph types.

---

### Auto Connect & Insert

![Auto Connect & Insert](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/AutoConnectInsert.gif)

Drag a node near other nodes and compatible pins are automatically connected when you release. These features are reimplemented natively in OctaGraph to work correctly with custom wire styles.

When the modifier is set to `None`, holding any modifier key (Alt, Ctrl, Shift) temporarily disables the feature, allowing you to drag freely without triggering auto-connect or insert.

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

![Insert on Wire](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/InsertOnWire.gif)

1. Start dragging a node
2. Move it over an existing wire
3. The wire highlights and preview connections appear
4. Release to insert the node into the wire (old wire is broken, two new connections are created)

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

![Bypass](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/Drag+X.gif)

![Bypass Selected](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/X.gif)

![Detach](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/Alt+X.gif)

---

### Graph Cleanup

![Cleanup](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/CleanupDisconnectedWires.gif)

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

![Editor Theme](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/OctaTheme.gif)

Customize the overall editor appearance with luminosity, saturation, and hue adjustments. Color transformations use the perceptually uniform LAB color space for accurate results.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Octa Theme | true | Toggle the editor theme |
| Theme Luminosity | 0 | Brightness adjustment (-100 to +100) |
| Theme Saturation | 0 | Color intensity (-100 to +100) |
| Theme Hue | 40 | Hue shift (0 - 360 degrees) |
| Keep Foreground Luminosity | false | Prevent text luminosity from shifting |

---

### Node Theme

![Node Theme](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/OctaGraph/Images/NodeTheme.gif)

Customize the appearance of graph nodes. Changing `Enable Node Theme` requires an editor restart.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Node Theme | true | Toggle node appearance customization (requires restart) |
| Var Node Opacity | 0.5 | Variable node background opacity (0.0 - 1.0) |
| Node Header Opacity | 0.25 | Header color overlay opacity (0.0 - 1.0) |
| Node Header Saturation | 1.0 | Header color saturation (0.0 - 1.0) |

---

### Compatibility

OctaGraph is compatible with [Blueprint Assist](https://www.fab.com/listings/14d7ba87-a587-406d-9369-ed75fa0a55ed) and [Node Graph Assistant](https://www.fab.com/listings/525a33bb-9b05-405d-bf3e-42ca990fb31b).

| Setting | Default | Description |
|---------|---------|-------------|
| Disable Conflicting Plugin Features | true | Automatically disable NGA's Auto Connect, Insert Node, Wire Style, and toolbar buttons on startup |

OctaGraph reimplements Auto Connect, Insert Node, and Bypass because NGA's versions don't work with custom wire styles. When `Disable Conflicting Plugin Features` is enabled, OctaGraph will automatically turn off the conflicting NGA features and save the config. NGA's other features (rearrange, select upstream/downstream, shake to disconnect, etc.) remain active.

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
| Hold any modifier while dragging | Auto Connect/Insert set to None | Temporarily disable auto-connect and insert |

*All keys and modifiers are configurable in settings. Bypass keys are ignored while typing in text fields.*

---

## FAQ

**Does this modify engine files?**
No. OctaGraph hooks into the editor's connection drawing pipeline at runtime. No engine source changes required.

**Can I use this with other graph editor plugins?**
Yes. OctaGraph is compatible with Blueprint Assist and Node Graph Assistant. Enable `Disable Conflicting Plugin Features` in settings to automatically resolve conflicts with NGA.

**Can I disable just the theme and keep the wires?**
Yes. Every feature category (wires, theme, node styling, auto-connect, bypass, cleanup) can be toggled independently.

**Does this affect packaged games?**
No. OctaGraph is editor-only and is not included in packaged builds.

**Can I switch back to default wires?**
Yes. Set `Wire Style` to `Default` in settings, or disable OctaGraph entirely with the `Enable OctaGraph` toggle.

**Why does changing Enable Node Theme require a restart?**
The node theme modifies Slate style brushes at startup. Disabling it at runtime doesn't restore the original brushes, so a restart is needed to apply the change cleanly.

**Can I temporarily disable auto-connect while dragging?**
Yes. When the modifier is set to `None`, holding any modifier key (Alt, Ctrl, Shift) temporarily suppresses auto-connect and insert-node.
