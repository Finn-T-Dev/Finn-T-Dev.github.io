---
title: 'UI Prototype with Noesis'
description: 'Developing a UI prototype using NoesisGUI Middleware'
image:
    url: '/images/NoesisProject/noesis-logo-blue.svg'
    alt: 'GitHub wallpaper'
platform: Unreal Engine 5
stack: Noesis Studio, NoesisGUI
---

# Noesis UI Implementation: Hierarchy Organization and Data Binding

Experimenting with the Noesis middleware for creating User Interfaces for video games. This project explores UI hierarchy organization and data binding challenges through implementing menu navigation and an in-game HUD.

## UI Hierarchy Organization

<img class="pro-img" src="/images/MainMenu_Hierarchy.png" alt="UI layout overview">

I organized the UI using a **modular, layered approach**:

**Main Menu Structure:**
- Root Grid container acts as the master layout
- Nested StackPanels for each menu section (Main Menu, Settings, Codex)
- Each component is self-contained, making it easy to modify individual elements without affecting others

**In-Game HUD Structure:**
- Spatial organization based on player eye movement patterns:
  - Health: Bottom-left (secondary priority)
  - Ammo counter: Bottom-right (primary weapon info location)
  - Compass: Top-center (navigation/orientation)
  - Kill count: Top-right (score tracking)
- Each HUD element is its own StackPanel anchored to specific screen positions
- This hierarchy ensures elements scale properly across different resolutions

<img class="pro-img" src="/images/UI_Layout_Noesis.png" alt="UI layout overview">

The modular hierarchy demonstrates separation of concerns - presentation (XAML), logic (Blueprint/C++), and data (view model) are kept distinct.

## Data Binding Challenge: Event-Driven HUD Updates

**The Challenge:**
The Unreal Engine FPS template uses a mix of Blueprint and C++ logic. I needed to:
1. Identify where game state data (health, ammo, kills) was stored
2. Disable the existing UMG HUD elements
3. Bind Noesis UI to the existing game logic without breaking the template's architecture

**My Approach:**

**Step 1: Traced the Data Flow**
- Found C++ event dispatchers in `ShooterCharacter.h`:
```cpp
  FBulletCountUpdatedDelegate OnBulletCountUpdated;
  FDamagedDelegate OnDamaged;
```
- These were already firing when game state changed, but were only connected to the old UMG widgets

**Step 2: Created a Data Context (View Model)**
- Built `BP_HUDData` Blueprint object to act as the view model
- Added properties: `Health`, `CurrentAmmo`, `MaxAmmo`, `Kills`, `CompassHeading`
- Created setter functions that trigger Noesis property change notifications

**Step 3: Connected Events to View Model**
- In `BP_ShooterPlayerController`, bound to character events in `OnPossess`:
```
  OnPossess → Cast to ShooterCharacter
           → Bind to OnBulletCountUpdated
           → Bind to OnDamaged
```
- This ensures bindings persist across character death/respawn

**Step 4: XAML Data Binding**
```xaml
<TextBlock Text="{Binding CurrentAmmo}" FontSize="48" Foreground="White"/>
```
- Direct binding to view model properties
- UI updates automatically when properties change

**Key Win: Event-Driven Updates**
Instead of polling game state every frame (Tick), the HUD updates only when values actually change. The C++ code broadcasts events (bullet fired, damage taken), which trigger view model updates, which automatically refresh the UI through Noesis bindings.

**Technical Challenge Solved:**
Initial issue - property changes weren't triggering UI updates. Solution: implemented `Noesis Notify Property Changed` in the setter functions, ensuring the binding system knows when to refresh displayed values.

**Performance Benefit:**
Event-driven approach means the UI only recalculates when necessary, not every frame, reducing overhead in a fast-paced FPS environment.

## Summary
- **Timeframe:** One week
- **Base:** Unreal Engine 5 FPS template
- **Challenge:** Navigating C++/Blueprint hybrid architecture, identifying and replacing legacy UMG HUD
- **Solution:** Leveraged existing event dispatchers, created clean separation between game logic and UI through view model pattern
- **Result:** Modular, maintainable UI with efficient event-driven updates
       

