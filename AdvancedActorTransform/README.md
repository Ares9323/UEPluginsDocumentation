# **Advanced Actor Transform - How to setup:**
Welcome to the updated version of AdvancedActorTransform, if you are looking for the documentation for the older version, it's still mantained in this repository but the first version is deprecated and will no longer be updated or distributed.

- Download AdvancedActorTransform from the [Unreal Marketplace](https://unrealengine.com/marketplace/en-US/product/26fa6336e06b41d2baad1f9308d9019b) and add it to your project
- Feel free to delete the ExampleContent folder in case you don't need it
- Click a column header of the following table to go to the documentation of the version you need:

|VERSION COMPARISON | [AAT 1.0](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedActorTransform/V1.0.md) | [AAT 2.0](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/AdvancedActorTransform/V2.0.md) |
|-------------------------------------------|-----------------------|-----------------------------------------------|
|Works at runtime                           | NO                    | YES                                           |
|Supports Instanced Static Meshes           | NO                    | YES                                           |
|Supports Particle Systems / Text / Lights  | YES                   | NO, Only static and skeletal meshes           |
|Supports many instances                    | No, it becomes laggy  | Tested with 250000 instances without issues   |
|Affects collision                          | Yes                   | No                                            |
|Instances can be controlled independently  | Yes, with tags        | Yes, with material instances                  |
|Easy to use                                | Yes, very basic setup | Requires a bit of experience with materials   |
|Supports distance from component           | Yes                   | Yes                                           |
|Supports distance from camera              | No                    | Yes                                           |
|Supports animation with timea              | No                    | Yes                                           |
|Supports Material Parameter Collections    | No                    | Yes                                           |