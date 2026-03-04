![Logo](https://github.com/Ares9323/UEPluginsDocumentation/blob/master/TonemapperSwapper/Images/Logo.png)

# Tonemapper Swapper
Replace Unreal Engine's default tonemapper with AgX or GT (Uchimura), two color-science-accurate tonemapping algorithms that deliver superior highlight rolloff, natural color handling, and consistent results across exposure ranges.

Available on [FAB](https://www.fab.com/portal/listings/aa0e0734-8877-47d6-9ab7-5d0f719467a2)

## How to activate
* Open the Plugins window
* Search for "Tonemapper Swapper"
* Activate the checkbox
* Restart the editor

## How to use
* Go to **Project Settings > Plugins > TonemapperSwapper**
* Change the **Tonemapper Mode** to "AgX", "GT (Uchimura)", or "Unreal Default"

### AgX
* Select a **Look** preset: Default (neutral), Saturated (punchy), or Custom
* In Custom mode, adjust Pre-Exposure Bias, Min/Max EV, Saturation, and per-channel Slope/Power/Offset (ASC CDL)

### GT (Uchimura)
* Select a **Look** preset: Default, High Contrast, or Custom
* In Custom mode, adjust Pre-Exposure Bias, Max Brightness, Contrast, Linear Start, Linear Length, Black Tightness, and Pedestal

## Notes
* The plugin overrides engine shaders in memory only — no engine files are modified
* AgX requires sRGB working color space (set automatically when AgX is selected)
* Compatible with UE 5.5, 5.6, and 5.7
