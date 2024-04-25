![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/ExposedCameraShakes/Images/Logo.png)

# Exposed Camera Shakes
Widgets and Utilities to improve your daily workflow in Unreal Engine
Available on the [Unreal Marketplace](https://unrealengine.com/marketplace/en-US/product/1f20aaa8b05e43be99c3be67bf5c7745)


## How to activate
* Open plugins
* Look for ExposedCameraShakes
* Activate the checkbox
* Restart the editor
* [WARNING], In collaborative projects any user needs to have the plugin installed, otherwise some classes might be orphaned and you'll get a lot of errors. You can create a "Plugins" folder in the project root and copy the plugin there, then you can upload it in your source control system.

## How to use

### Open file in windows explorer
* Create a new camera shake BP that inherits from ExposedDefaultCameraShakeBase
* Create a new camera shake pattern BP that inherits from ExposedPerlinNoiseCameraShakePattern
