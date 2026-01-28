---
title: 'UI Prototype with Noesis'
description: 'Developing a UI prototype using NoesisGUI Middleware'
image:
    url: '/images/NoesisProject/noesis-logo-blue.svg'
    alt: 'GitHub wallpaper'
platform: Unreal Engine 5
stack: Noesis Studio, NoesisGUI
---

# Noesis UI Implementation

Built a menu system and in-game HUD using Noesis middleware on top of the UE5 FPS template.

## UI Hierarchy

<img class="pro-img" src="/images/MainMenu_Hierarchy.png" alt="UI layout overview">

**Menu structure:**
- Root Grid with nested Grids and/pr StackPanels for each section
- Each menu (Main, Settings, Codex) is self-contained
- Button commands bound directly to Blueprint functions
- Reusable (but ugly) button template for consistent styling

**HUD layout:**
- Health: bottom-left
- Ammo: bottom-right  
- Compass: top-center
- Kills: top-right

Each element is anchored such that they scale properly across resolutions.

<img class="pro-img" src="/images/UI_Layout_Noesis.png" alt="UI layout overview">

## Data Binding Challenges

### Challenge 1: Event-Driven HUD Updates

The FPS template mixes Blueprint and C++, so I had to find where the game data lived and how to connect it to Noesis.

**What I did:**
1. Found the C++ event dispatchers (`OnBulletCountUpdated`, `OnDamaged`) that fire when game state changes
2. Created `BP_HUDData` object to hold UI values (health, ammo, kills, compass)
3. Bound to the character events in `OnPossess` (so it works after respawn)
4. Added setter functions that call `Noesis Notify Property Changed`
5. Used `{Binding PropertyName}` in XAML to connect to the data

The HUD updates only when values actually change (event-driven), not every frame. Main issue: properties weren't updating until I added the notify calls in the setter functions.

### Challenge 2: Populating the Codex

Created a data structure to hold codex entries and populate them dynamically.

**What I did:**
1. Created `BP_CodexEntry` struct with fields for title, description, image path. These contain data relating to character bios.
2. Built an array of these entries in the view model
3. Used a `ListBox` in XAML with `ItemsSource="{Binding CodexEntries}"`
4. Created a DataTemplate to define how each entry displays
5. The view model populates the entries on initialisation

This meant I could add/modify codex content without touching the XAML.

### Challenge 3: Two-Way Binding for Volume Slider

The settings menu needed a volume slider that both reads and writes to the game's audio settings.

**What I did:**
1. Added `Volume` property to the settings view model
2. Used `{Binding Volume, Mode=TwoWay}` on the Slider in XAML
3. When the slider moves, it updates the view model property
4. The setter function applies the volume change to UE5's audio system
5. Initial value is read from saved settings when the menu opens

Two-way binding meant the slider position always matches the actual game volume, and dragging it immediately updates the value in-engine.

## Summary
- One week project
- Had to disable the existing UMG HUD and figure out the template's data flow
- Used existing event dispatchers instead of polling every frame where possible
- Data structures and binding patterns made content dynamic and maintainable
- Two-way binding kept UI and game state in sync
       

