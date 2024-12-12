![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedRestartEditor/Images/Logo.png)

## **Restart Unreal Editor [FREE VERSION] - How to use the plugin:**
- Download the plugin from [FAB](https://www.fab.com/listings/2e260da0-4a02-4f7b-8b97-3f783dc025f1)
- Enable the plugin in the Editor "Plugins" window
- Restart the editor
- You should have an icon in the top bar, click it or press CTRL+SHIFT+R to restart the editor.
- If you want to enable by default the extension for all your project, edit the "RestartEditor.uplugin" file that you can find in the folder: "Engine/Plugins/Marketplace/RestartEditor" and set "EnabledByDefault" to true, otherwise, you could use [this amazing tool to Disable and Enable plugins by default](https://github.com/DarknessFX/UEPlugins_DisableDefault).

## **Advanced Restart Editor [PAID VERSION] - How to use the plugin:**
- Download the plugin from [FAB](https://www.fab.com/listings/2c59b825-08fc-45bb-94cb-3413bb7ba8af)
- Enable the plugin in the Editor "Plugins" window
- Restart the editor
- You should have an icon in the top bar, click it or press CTRL+ALT+R to restart the editor.
- Press CTRL+ALT+SHIFT+R to force restart the editor, no prompt to save file changes will show up.
- In Editor Settings you can change the behaviour of the extension from the Plugins tab section, select "Advanced Restart Editor Plugin"
![SettingsImage](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedRestartEditor/Images/Settings.png)
  - Look for Multiple Instances on Startup, if true the plugin will check if another instance of the editor is already running, if true it will ask you if you want to close it or continue opening it.
  - Allow Multiple Instances of same Project, if false the plugin will automatically close the other instance of the editor if you try to open the same project.
  - Show Notification on Auto Close, if true the plugin will show a notification when it closes the other instance of the editor.
  - Show Debug Dialogs, if true the plugin will show a debug dialog whenever a plugin action is performed.

- If you want to enable by default the extension for all your project, edit the "RestartEditor.uplugin" file that you can find in the folder: "Engine/Plugins/Marketplace/AdvancedRestartEditor" and set "EnabledByDefault" to true, otherwise, you could use [this amazing tool to Disable and Enable plugins by default](https://github.com/DarknessFX/UEPlugins_DisableDefault).





