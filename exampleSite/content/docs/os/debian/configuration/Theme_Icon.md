---
title: "Theme and Icon Installation"
description: "Tutorial on installing and applying custom themes and icon sets in Debian, including downloading themes from online sources and configuring appearance settings."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

Custom themes and icon sets allow you to personalize the appearance of your Debian desktop environment. By installing and applying these customizations, you can enhance the visual aesthetics and create a unique desktop experience tailored to your preferences. This tutorial provides detailed instructions for installing and applying custom themes and icon sets in Debian, including downloading themes from online sources and configuring appearance settings.

## Prerequisites

Before you begin, ensure you have:

- Debian installed and logged into the desktop environment.
- Basic familiarity with navigating the Debian desktop environment and using a terminal.

## Step 1: Download Themes and Icons

1. **Open a Web Browser**: Use your preferred web browser to search for custom themes and icon sets.
2. **Explore Websites**: Visit websites that offer themes and icons, such as:
   - [GNOME-Look](https://www.gnome-look.org)
   - [Pling](https://www.pling.com)
   - [Xfce-Look](https://www.xfce-look.org)
3. **Download Themes and Icons**: Browse through available themes and icons, selecting and downloading the ones you like. These usually come in compressed formats like `.zip`, `.tar.gz`, or `.tar.bz2`.

## Step 2: Extract Theme and Icon Archives

1. **Locate Downloads**: Navigate to the folder where you downloaded the theme and icon archives (usually your `Downloads` folder).
2. **Extract Archives**: Use your file manager or terminal to extract the theme and icon archives:
   - **Using a Terminal**:
     ```bash
     cd ~/Downloads
     tar -xvf theme-name.tar.gz      # For .tar.gz files
     unzip icon-name.zip             # For .zip files
     ```
3. **Move Extracted Folders**: Move the extracted folders to the appropriate directories:
   - **Themes**: Move to `~/.themes` (create this directory if it doesn't exist).
     ```bash
     mkdir -p ~/.themes
     mv extracted-theme-folder ~/.themes/
     ```
   - **Icons**: Move to `~/.icons` (create this directory if it doesn't exist).
     ```bash
     mkdir -p ~/.icons
     mv extracted-icon-folder ~/.icons/
     ```

## Step 3: Install GNOME Tweaks Tool

1. **Open Terminal**: Launch a terminal window.
2. **Install GNOME Tweaks**: Enter the following command to install the GNOME Tweaks tool:
   ```bash
   sudo apt install gnome-tweaks
   ```

## Step 4: Apply Themes and Icons

1. **Open GNOME Tweaks**: Launch the GNOME Tweaks tool from the application menu.
2. **Navigate to Appearance**: Click on the "Appearance" or "Themes" section.
3. **Select Themes and Icons**:
   - Use the dropdown menus to select the downloaded themes for the following options:
     - **Applications Theme**
     - **Cursor Theme**
     - **Shell Theme** (if applicable)
     - **GTK Theme** (if applicable)
   - Select your preferred icon theme from the "Icons" dropdown menu.

## Step 5: Customize Appearance Settings

1. **Explore Additional Settings**: Use the GNOME Tweaks tool to further customize your appearance settings.
2. **Adjust Options**: Customize settings such as:
   - Font settings
   - Window title bars
   - Interface scaling
3. **Apply Changes**: After making adjustments, ensure to apply the changes to see the effects.

## Step 6: Test Appearance Changes

1. **Verify Changes**: Open various applications and system windows to check that the selected themes and icons are applied correctly.
2. **Adjust if Necessary**: If any changes do not appear as expected, revisit GNOME Tweaks to make adjustments.

## Step 7: Apply System-wide Themes (Optional)

1. **Copy to System Directories**: For themes you wish to apply system-wide, copy the extracted theme folders to the following directories:
   - Themes: `/usr/share/themes`
   - Icons: `/usr/share/icons`
   ```bash
   sudo cp -r ~/.themes/theme-folder /usr/share/themes/
   sudo cp -r ~/.icons/icon-folder /usr/share/icons/
   ```
2. **Select System-wide Themes**: Use the GNOME Tweaks tool or other system settings utilities to choose the system-wide themes and icons.

## Conclusion

By installing and applying custom themes and icon sets in Debian, you can personalize your desktop environment and create a visually stunning desktop experience. Experiment with different themes and icons to find the combination that best suits your style and preferences. Enjoy your newly customized Debian setup!