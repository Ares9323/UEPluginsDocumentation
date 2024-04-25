![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/Logo.png)

# AdvancedEditorUtilities
Widgets and Utilities to improve your daily workflow in Unreal Engine
Available on the [Unreal Marketplace](https://unrealengine.com/marketplace/en-US/product/f375645593fc4d909bf8c79b9f64a066)


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

* You can edit the "Common strings to search" array to change the dropdown menu in the extension:

![CommonStrings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStrings.png)

* You can also assign them a shortcut to launch the filter automatically:

![CommonStringsDropdown](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/CommonStringsDropdown.png) ![FindInBlueprints](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/FindInBlueprints.png)

* The other settings are also changeable from here, but they can be modified through their own widgets, so I don't really recommend doing it from here:

![WidgetSettings](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedEditorUtilities/Images/WidgetSettings.png)

* You can also edit them in a permanent way, by editing the `DefaultCommands` and `DefaultViewModes` arrays in C++ by editing `AdvancedEditorUtilitiesSettings.h` (**WARNING: you need to move the plugin from the Marketplace folder into a project "Plugins" folder to recompile it, then you can move it back but you might lose your settings if you update the plugin from the Epic Launcher**)
