![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/SDL_EnhancedInput/Images/Logo.png)

# SDL Enhanced Input

Bridges SDL3 gamepad and joystick input into Unreal Engine's Enhanced Input system, unlocking full support for controllers that UE doesn't handle natively — including DualSense adaptive triggers, motion sensors, touchpad, racing wheels, flight sticks, arcade controllers, and Nintendo Wiimotes.

Available on [FAB](https://www.fab.com/)

---

## Installation

1. Install the plugin from FAB
2. Open **Edit > Plugins**
3. Search for **SDL Enhanced Input**
4. Enable the checkbox
5. Restart the editor
6. Connect a controller — it's automatically detected and ready to use

## Settings

All settings are in **Edit > Project Settings > Plugins > SDL Enhanced Input**.

---

## Supported Devices

| Device | Features |
|--------|----------|
| **PS5 (DualSense)** | Adaptive triggers, touchpad, motion sensors, lightbar LED |
| **PS4 (DualShock 4)** | Touchpad, motion sensors, lightbar LED |
| **PS3** | Standard gamepad input |
| **Xbox 360 / One / Series** | Standard gamepad, trigger rumble (Xbox One+) |
| **Switch Pro Controller** | Standard gamepad, LED |
| **Joy-Cons (paired)** | Standard gamepad |
| **GameCube (adapter)** | Standard gamepad |
| **Racing Wheels** | Force feedback, RPM LEDs (Logitech G29/G920+) |
| **Flight Sticks / HOTAS** | All axes, buttons, hats, force feedback |
| **Arcade Sticks** | Buttons and stick via raw joystick |
| **Nintendo Wiimote** | BT scanning, buttons, accel/gyro, Nunchuck, IR tracking (Windows only, requires a sensor bar or any two IR emitters — even two candles work) |
| **Generic HID** | Up to 24 buttons, 8 axes, 4 hats |

**Tested devices:** DualShock 4, DualSense, Xbox 360, Xbox One, Nintendo Wiimote (with and without MotionPlus and Nunchuck), single Joy-Con, paired Joy-Cons, Switch Pro Controller, Logitech G29, Microsoft SideWinder (X05-63895)

---

## Features

### DualSense Adaptive Triggers

Control the resistance of L2/R2 triggers on PS5 DualSense controllers directly from Blueprint.

| Function | Description |
|----------|-------------|
| `SetDualSenseTriggers` | Set left/right trigger effects (Feedback, Weapon, Vibration) |
| `ClearDualSenseTriggers` | Reset triggers to default |
| `IsDualSense` | Check if a controller is a DualSense |

**Effect types:**

- **Feedback** — Continuous resistance from a start position with configurable strength
- **Weapon** — Two-stage resistance simulating a trigger pull with a click point
- **Vibration** — Vibrating resistance across a configurable zone

<!-- Screenshot: DualSense trigger effect in Blueprint -->

---

### Motion Sensors

Gyroscope (3-axis) and accelerometer (3-axis) exposed as Enhanced Input axes. Works on DualSense, DualShock 4, Switch Pro, and Wiimote.

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Motion In Editor | false | Allow motion input in PIE |
| Gyro Deadzone | 0.01 | Threshold below which gyro is zeroed |
| Accel Deadzone | 0.02 | Threshold below which accel is zeroed |

**Auto-calibration:** The plugin samples the first 50 gyro readings at startup to compute a drift offset. Use `SDL.MotionCalibrate` or `CalibrateMotionSensors()` for manual recalibration.

<!-- Screenshot: Motion sensor debug widget -->

---

### Touchpad Input

Two-finger multi-touch tracking on DualSense and DualShock 4.

| FKey | Description |
|------|-------------|
| `SDLTouchpad_Finger1X/Y` | First finger position (-1 to 1) |
| `SDLTouchpad_Finger2X/Y` | Second finger position (-1 to 1) |
| `SDLTouchpad_Finger1Touch` | First finger touching (bool) |
| `SDLTouchpad_Finger2Touch` | Second finger touching (bool) |
| `SDLTouchpad_Click` | Touchpad pressed (bool) |

<!-- Screenshot: Touchpad visualization widget -->

---

### Wiimote Support (Windows Only)

Full Nintendo Wiimote integration via direct Bluetooth HID connection.

| Function | Description |
|----------|-------------|
| `StartWiimoteScan` | Begin Bluetooth scanning for Wiimotes |
| `StopWiimoteScan` | Stop ongoing scan |
| `IsWiimoteScanning` | Check scan status |
| `GetWiimoteCount` | Number of connected Wiimotes |

**Supported inputs:**

- All buttons (A, B, 1, 2, +, -, Home, D-Pad)
- Accelerometer (3-axis)
- Gyroscope (3-axis, requires MotionPlus)
- Nunchuck analog stick + Z/C buttons
- IR sensor — 2-dot tracking for pointer-style input

| Setting | Default | Description |
|---------|---------|-------------|
| Enable Wiimote | true | Toggle Wiimote support |
| Manual Scan Duration | 30.0 | Default scan duration in seconds |
| Nunchuck Deadzone | 0.05 | Nunchuck analog stick deadzone |
| IR Deadzone | 0.005 | IR sensor deadzone |

<!-- Screenshot: Wiimote with Nunchuck 3D model -->

---

### Advanced Haptics / Force Feedback

11 haptic effect types with handle-based lifecycle management. Works on any SDL device with haptic support (wheels, joysticks, gamepads).

| Function | Description |
|----------|-------------|
| `CreateHapticEffect` | Create an effect, returns a handle |
| `PlayHapticEffect` | Play by handle with iteration count |
| `UpdateHapticEffect` | Modify a running effect |
| `StopHapticEffect` | Stop a single effect |
| `StopAllHapticEffects` | Stop all effects on a device |
| `DestroyHapticEffect` | Free the effect handle |
| `GetHapticCapabilities` | Query supported effects and limits |
| `SetHapticAutocenter` | Set wheel autocenter strength (0-100) |
| `SetHapticGain` | Set global haptic gain (0-100) |

**Effect types:** Constant, Sine, Triangle, Sawtooth Up/Down, Spring, Damper, Friction, Inertia, Ramp, Custom

---

### Racing Wheel LEDs

Control Logitech RPM indicator LEDs on compatible wheels (G29, G920, etc.).

| Function | Description |
|----------|-------------|
| `SetWheelLEDPattern` | Set LEDs with a 5-bit bitmask (0-31) |
| `SetWheelLEDPercent` | Set LEDs as a tachometer fill (0.0-1.0) |

---

### LED Control

Set the lightbar color on DualSense, DualShock 4, Switch Pro, and other controllers with RGB LEDs.

| Function | Description |
|----------|-------------|
| `SetGamepadLED` | Set RGB color (0-255 per channel) |

---

### Rumble

| Function | Description |
|----------|-------------|
| `Rumble` | Large motor + small motor with duration |
| `RumbleTriggers` | Left/right trigger rumble (Xbox One+) |

---

### Controller Info

Query device metadata at runtime.

| Function | Returns |
|----------|---------|
| `GetControllerInfo` | Full device info (name, type, VID/PID, battery, haptic support) |
| `GetControllerType` | Device type enum (PS5, Xbox, Wheel, FlightStick, etc.) |
| `GetBatteryPercent` | Battery level (0-100) |
| `GetConnectedControllerCount` | Number of connected devices |
| `GetAllConnectedDevices` | Array of all device info structs |

**Connection events:**

| Delegate | Description |
|----------|-------------|
| `OnControllerConnected` | Fires with slot index and device info |
| `OnControllerDisconnected` | Fires with slot index |

---

### Virtual Joystick

Simulate controller input without physical hardware using console commands. Useful for testing all 24 buttons and 8 axes.

| Command | Description |
|---------|-------------|
| `SDL.SimButton <index> [0\|1]` | Press/release a button (1-24), toggle if no value |
| `SDL.SimAxis <index> <value>` | Set an axis value (1-8, range -1.0 to 1.0) |
| `SDL.SimDestroy` | Remove the virtual joystick |

---

### Multi-Controller

Supports up to 8 gamepads and 4 raw joysticks simultaneously.

| Setting | Default | Description |
|---------|---------|-------------|
| Force All Gamepads To Player 0 | false | Route all gamepad input to a single player |

**Slot ranges:**

| Range | Device Type |
|-------|-------------|
| 0 - 7 | Auto-detected gamepads/joysticks |
| 100+ | Wiimote devices (100 = Wiimote 1, 101 = Wiimote 2, ...) |
| 200+ | Explicit raw joystick access (200 = Joystick 0, 201 = Joystick 1, ...) |

---

## Custom FKeys

All custom FKeys are registered at startup and available in Input Mapping Contexts.

### Joystick

| FKey | Count | Description |
|------|-------|-------------|
| `SDLJoystick_Axis0` - `Axis7` | 8 | Raw joystick axes |
| `SDLJoystick_Button0` - `Button23` | 24 | Raw joystick buttons |
| `SDLJoystick_Hat0Up/Down/Left/Right` - `Hat3*` | 16 | D-pad / hat switches |

### Motion Sensors

| FKey | Description |
|------|-------------|
| `SDLMotion_AccelX/Y/Z` | Accelerometer axes |
| `SDLMotion_GyroX/Y/Z` | Gyroscope axes |

### Gamepad Extras

| FKey | Description |
|------|-------------|
| `SDLGamepad_Guide` | PS / Xbox / Home button |
| `SDLGamepad_Misc1` - `Misc6` | Extra buttons (Share, Mute, etc.) |
| `SDLGamepad_LeftPaddle1/2` | Left back paddles |
| `SDLGamepad_RightPaddle1/2` | Right back paddles |

### Touchpad

| FKey | Description |
|------|-------------|
| `SDLTouchpad_Finger1X/Y`, `Finger1Touch` | First finger |
| `SDLTouchpad_Finger2X/Y`, `Finger2Touch` | Second finger |
| `SDLTouchpad_Click` | Touchpad press |

### Wiimote IR

| FKey | Description |
|------|-------------|
| `SDLWiimote_IR_Dot1X/Y`, `Dot1Visible` | First IR dot |
| `SDLWiimote_IR_Dot2X/Y`, `Dot2Visible` | Second IR dot |
| `SDLWiimote_IR_Visible` | Any IR dot visible (composite) |

---

## Console Commands

| Command | Usage | Description |
|---------|-------|-------------|
| `SDL.WiimoteScan [seconds]` | `SDL.WiimoteScan 30` | Start Bluetooth scan for Wiimotes |
| `SDL.WiimoteScanStop` | `SDL.WiimoteScanStop` | Stop ongoing scan |
| `SDL.MotionCalibrate` | `SDL.MotionCalibrate` | Recalibrate gyro/accel |
| `SDL.SetLED <R> <G> <B> [slot]` | `SDL.SetLED 255 0 0` | Set gamepad LED color |
| `SDL.SetTrigger <type> [params]` | `SDL.SetTrigger Feedback 2 5` | DualSense adaptive trigger |
| `SDL.Haptic <type> [str] [dur] [slot]` | `SDL.Haptic Sine 0.8 500` | Play haptic effect |
| `SDL.HapticInfo [slot]` | `SDL.HapticInfo 0` | Show haptic capabilities |
| `SDL.SetWheelLED <pattern> [slot]` | `SDL.SetWheelLED 15` | Logitech wheel RPM LEDs |
| `SDL.SimButton <idx> [0\|1]` | `SDL.SimButton 1` | Simulate virtual joystick button |
| `SDL.SimAxis <idx> <value>` | `SDL.SimAxis 1 0.5` | Simulate virtual joystick axis |
| `SDL.SimDestroy` | `SDL.SimDestroy` | Destroy virtual joystick |

---

## SDL Driver Hints

Advanced settings to control which SDL input drivers are active. Found in **Project Settings > Plugins > SDL Enhanced Input** under the driver sections.

All hints use a tristate value: **Default** (let SDL decide), **Enabled**, or **Disabled**.

<details>
<summary>Driver Hint List</summary>

**System drivers:** DirectInput, RawInput, WGI, HIDAPI, GameInput, JoystickThread

**Vendor HIDAPI:** PS3, PS4, PS5, Nintendo Switch, Joy-Con, GameCube, Xbox

**Vendor features:** PS player LEDs, PS5 rumble, Switch player LEDs, home button LED

**Specialty:** Luna, Stadia, Steam Controller/Deck, Shield, 8BitDo, Zuiki, Flydigi

**Wheel:** Logitech LG4FF force feedback

**General:** AllowBackgroundEvents, RawInputCorrelateXInput, EnhancedReports, ROGChakram

**Advanced:** Additional custom hints as key-value pairs

</details>

---

## Example Content

The plugin includes 160+ example assets to get you started:

### Input Actions & Mapping Contexts

| Asset | Description |
|-------|-------------|
| `IMC_SDL_Gamepad` | Standard gamepad (sticks, triggers, buttons, D-pad, shoulders) |
| `IMC_SDL_Motion` | Accelerometer + gyroscope (3 axes each) |
| `IMC_SDL_Touchpad` | Two-finger touch + click |
| `IMC_SDL_Wiimote` | Wiimote buttons + IR dots (reuses gamepad IAs) |
| `IMC_SDL_Joystick` | Raw joystick (8 axes, 24 buttons) |

40+ Input Actions are pre-configured covering every input type.

### Blueprints

| Asset | Description |
|-------|-------------|
| `BP_SDL_Character` | Player character wired to SDL input |
| `BP_C_DS5` | DualSense 3D model with per-button highlighting |
| `BP_C_G29` | Logitech G29 wheel model |
| `BP_C_WiiMote` | Wiimote + Nunchuck model |
| `BP_C_Cloche` | Flight stick model |
| `GM_SDL_Example` | Example game mode |
| `LV_SDL_Example` | Example level |

### Debug UI Widgets

| Widget | Description |
|--------|-------------|
| `WBP_SLD_UI` | Main debug panel with full controller status |
| `WBP_AxisVisualizer` | Axis bar display |
| `WBP_ButtonVisualizer` | Button state indicator |
| `WBP_HatVisualizer` | D-pad / hat visualizer |

<!-- Screenshot: Debug UI panel showing all inputs -->

<!-- Screenshot: 3D controller models in example level -->

---

## Blueprint API Reference

### DualSense

| Function | Description |
|----------|-------------|
| `SetDualSenseTriggers(Slot, Left, Right)` | Set adaptive trigger effects |
| `ClearDualSenseTriggers(Slot)` | Reset to default |
| `IsDualSense(Slot)` | Check controller type |

### Controller Info

| Function | Description |
|----------|-------------|
| `GetControllerInfo(Slot)` | Full device metadata |
| `GetControllerType(Slot)` | Device type enum |
| `GetBatteryPercent(Slot)` | Battery level |
| `GetConnectedControllerCount()` | Connected device count |
| `GetAllConnectedDevices()` | All device info structs |

### Wiimote

| Function | Description |
|----------|-------------|
| `StartWiimoteScan(Duration)` | Begin BT scan |
| `StopWiimoteScan()` | Stop scan |
| `IsWiimoteScanning()` | Check scan status |
| `GetWiimoteCount()` | Connected Wiimote count |

### Per-Device Polling

| Function | Description |
|----------|-------------|
| `GetControllerButtonState(Slot, Index)` | Button state (bool) |
| `GetControllerAxisValue(Slot, Index)` | Axis value (-1 to 1) |
| `GetControllerHatValue(Slot, Index)` | Hat bitmask |
| `GetControllerAccelerometerValue(Slot)` | Accel FVector |
| `GetControllerGyroscopeValue(Slot)` | Gyro FVector |
| `GetControllerTouchpadValue(Slot, Finger, bTouching)` | Touch FVector2D |
| `GetControllerIRValue(Slot, Dot, bVisible)` | IR FVector2D |

### Haptics

| Function | Description |
|----------|-------------|
| `CreateHapticEffect(Slot, Effect)` | Create effect → handle |
| `PlayHapticEffect(Slot, Handle, Iterations)` | Play effect |
| `UpdateHapticEffect(Slot, Handle, Effect)` | Update running effect |
| `StopHapticEffect(Slot, Handle)` | Stop effect |
| `DestroyHapticEffect(Slot, Handle)` | Free handle |
| `StopAllHapticEffects(Slot)` | Stop all |
| `SetHapticAutocenter(Slot, Value)` | Wheel autocenter (0-100) |
| `SetHapticGain(Slot, Value)` | Global gain (0-100) |
| `GetHapticCapabilities(Slot)` | Query device capabilities |

### Rumble & LEDs

| Function | Description |
|----------|-------------|
| `Rumble(Slot, Large, Small, Duration)` | Motor rumble |
| `RumbleTriggers(Slot, Left, Right, Duration)` | Xbox trigger rumble |
| `SetGamepadLED(Slot, R, G, B)` | Lightbar color |
| `SetWheelLEDPattern(Pattern, Slot)` | Wheel RPM LEDs (bitmask) |
| `SetWheelLEDPercent(Percent, Slot)` | Wheel RPM LEDs (fill) |

### Utility

| Function | Description |
|----------|-------------|
| `SetSDLHint(Name, Value)` | Set SDL hint at runtime |

---

## FAQ

**Does this replace UE's built-in input?**
No. The plugin registers alongside UE's native input devices. Standard gamepad buttons map to `FGamepadKeyNames`, so existing Input Actions work unchanged. The plugin adds new FKeys for features UE doesn't expose.

**Does this modify engine files?**
No. SDL3 is loaded as a dynamic library at runtime.

**Can I use this with local multiplayer?**
Yes. Up to 8 gamepads and 4 raw joysticks, each assigned to a separate player slot.

**Do I need to configure SDL driver hints?**
No. The defaults work for most controllers. The hints are for edge cases like forcing a specific driver for niche hardware.

**Does the Wiimote work on macOS or Linux?**
Not currently. Wiimote uses Windows Bluetooth APIs and direct HID. The rest of the plugin could support other platforms when SDL3 builds are provided.

**Can I test without a physical controller?**
Yes. Use `SDL.SimButton` and `SDL.SimAxis` to simulate a virtual joystick with 24 buttons and 8 axes.

**What happens if I uninstall the plugin?**
Nothing breaks. The plugin doesn't modify any engine files, project settings, or saved data. Input Actions referencing custom FKeys will simply stop receiving input.
