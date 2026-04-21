# sweet-transparent-toolbar-color-fix
Kvantum Sweet Transparent Toolbar Color Issue (Plasma + Kvantum + Sweet Transparent Toolbar)

## Overview

This document describes an issue in KDE Plasma when using the Sweet Transparent Toolbar Kvantum theme. The problem affects how UI colors respond to wallpaper changes, especially inside Dolphin file manager.

Even when Plasma is configured to change colors based on wallpaper, some UI elements do not update correctly.

 **Issue**:

* Dolphin keeps a purple accent color after wallpaper changes
* Folder icons and selection highlights remain purple
* Right-click menus and selection outlines also keep the same accent color
* Other parts of the system update normally, but Kvantum-themed elements do not

## Cause

The issue is related to Kvantum theme configuration:

* The Sweet Transparent theme uses predefined color settings in its configuration files
* Some UI elements (like selection highlights and toolbar accents) are not fully linked to Plasma’s dynamic color system
* As a result, Plasma changes wallpaper colors, but Kvantum (Sweet) keeps using its own stored theme colors (purple accent in this case)

## Simple Fix

The fix was done by replacing or restoring Kvantum theme configuration files.

**1.Download theme files**:


The corrected theme files (same names as original Kvantum theme files) must be obtained:

* `Sweet-transparent-toolbar.kvconfig`
* `Sweet-transparent-toolbar.svg`

**2.Place files in Kvantum config directory**

Copy the files into:

```bash
~/.config/Kvantum/Sweet-transparent-toolbar/
```

Replace existing files if asked.

**3. Apply theme:**


After placing the files:

* Open Kvantum Manager
* Select “Sweet Transparent Toolbar” theme
* Apply changes
* Restart Plasma session or log out and log in

After applying the corrected files:

* Dolphin selection color follows Plasma system colors
* Purple fixed accent issue is removed
* Toolbar and UI elements better match wallpaper-based color changes



## What I changed

I edited the Kvantum theme configuration file inside:

```bash
~/.config/Kvantum/Sweet-transparent-toolbar/
```

The main change was removing or commenting out several **hard-coded color overrides** in the `[GeneralColors]` section. These included fixed theme values for items like highlight, text, button, and window colors.

Before the change, these values were forcing the theme to stay on a fixed purple accent instead of following the Plasma system color scheme.

After removing those overrides, Kvantum was able to fall back to Plasma’s default dynamic colors, which allowed the toolbar, Dolphin selection highlights, and other UI elements to update correctly when the wallpaper or system color scheme changed.


## Conclusion

The issue was caused by Kvantum theme files not fully respecting Plasma’s dynamic color system. Replacing the theme configuration files restored proper color inheritance from the system, allowing Dolphin and other UI components to update correctly with wallpaper changes.
