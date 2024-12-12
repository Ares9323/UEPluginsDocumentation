![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/ExposedCameraShakes/Images/Logo.png)

# Exposed Camera Shakes
Change the values of your camera shakes at runtime in a few steps without the need of C++
Available on [FAB](https://www.fab.com/listings/69664d4f-7163-4768-82cf-48b86d9fa859)


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
* Look at the example blueprint to see how to interact with the active camera shake
