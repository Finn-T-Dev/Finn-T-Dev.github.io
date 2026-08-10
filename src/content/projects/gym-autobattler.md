---
title: 'Gym-Themed Autobattler Prototype'
description: 'Devising system structure for gym-themed autobattler game inspired by The Bazaar & Balatro'
image:
    url: '/images/GitHub.webp'
    alt: 'GitHub wallpaper'
platform: PC
stack: Unreal Engine 5, NoesisGUI
---

## Overview
An autobattler that pits you (the player) against fierce athletes in the gym in pursuit of life's paramount achievement: Gym Alpha. Choose from a diverse range of playable characters and set off on your journey to claim the ultimate prize. You'll need to prepare, plan and perform if you want to surpass your competition in all 8 workouts. Position your items on the dumbbell rack to harness synergies and maximise your power, learn new exercises from gym legends and purchase supplements from questionable vendors to enhance your gains. Your enemies will be doing whatever it takes, will you?

## Product Objectives
- Practical application of game balancing methodology
- Give the player meaningful options that add layers of strategic depth
- Incorporate gym culture and humour to appeal to the core target audience

## Gameplay Pillars
- **Autonomous Combat:** Players arrange their items on the dumbbell rack. Items act autonomously during combat
- **Planning Ahead:** In the HUD, players can see a preview of the combat encounters they will face in the current stage (like in Balatro). Players will need to be able to strategically pivot to secure victory against a range of threats.
- **Buff yourself vs sabotage your opponent:** Some items will allow you to sabotage your opponent's equipment, bringing their gains potential down. Balance this with enhancing your own strength to get the best of both worlds.
- **Play what you get:** In the Iron Temple, no two workouts are the same (much to the chagrin of the Science Based Lifter, who deifies progressive overload).

## Narrative
In the modern commercial gym, people from all walks of life congregate to bask in the gifts brought to us by the Iron Lords and better themselves. Some of these gymgoers, however, are better than others. The best of the best have summitted the lofty social peaks and become Gym Alphas, a title regarded with the utmost respect, and a sprinkling of fear.

You play as a challenger, here to disrupt the status quo. Build your legend through intense preparation and the commitment to do whatever it takes to assume your rightful place at the top. Achieve otherworldly strength as the Strongman, alien aesthetics as the Science Based Lifter, or endless endurance as the Fitness Fanatic. Through planning, adaptability and a rigorous application of elbow grease, you will learn if you have what it takes to bring down the very best.

## Visuals
LIFT-OFF is heavily inspired by the Bazaar, my personal favourite autobattler. The gameplay driven purely by the UI, which needs to clearly convey the game state while preserving the visual theming. As I am no visual artist and this is a solo project, the plan is to use a combination of placeholder images and simple 3D models created in Blender or use primitives in the UE5 editor.

<img class="pro-img" src="/images/gym-autobattler/the-bazaar-board-layout.jpeg" alt="The Bazaar's UI Layout">

## Target Audience
LIFT-OFF's primary audience is the surprisingly large overlap between people who train at the gym and play video games, particularly those in their late teens to early thirties.

## Competitors
1. **The Bazaar:** Closest match in terms of gameplay, many of my gameplay systems are at least loosely based on the Bazaar. 
2. **Gym Simulator & Gym Empire:** Existing titles that tap in the gaming gymgoer market. These titles are thematically aligned with my project, but differ at a core gameplay level.

## Core Gameplay Loop
- Stage begins: Each encounter begins with taking stock of items in possession and looking ahead at the predetermined combat encounters ahead (events between designated combat encounters are hidden).
- Select an encounter from the 3 pseudorandomly generated events and resolve it for its effect (could be a merchant, selecting a buff if certain gameplay conditions have been met, or a miniboss etc)
- Acquire items and place them in strategic locations (items with active effects go in the dumbbell rack, items with passive effects (skills) are automatically placed in the gym bag)
- Repeat until the next combat encounter. In the standard case, there will be a mini-boss encounter at the halfway point of each stage.
- Continue to resolve encounters until the main boss of the stage. The victory condition for a stage is reducing the boss enemy's health bar to 0 before yours reaches 0 (ties are friendly).

## Gameplay Details
### Item positioning
The player and enemy combat areas will each be a 2-row grid, that expands up to a cap with player level. If placed on the top row, some items will target your opponent. For example, opponents who abuse steroids will have high blood toxicity levels, and will be inflicting damage over time effects on themselves. One possible player response would be to use an item that synergises with the toxicity, amplifying the steroid's negative side effects and hastening their defeat.

How you position your items can make or break a run. While poor item placement will not debuff the items you have, you may be missing out on vital placement bonuses. One example is items that work together to perform a real world function, such as a combination of a pre-workout supplement and warm-up routine enhancing the subsequent workout. When positioned adjacent to one another, your synergising items may receive a boost to ramp-up speed, raw stats or scaling. Synergies are not just limited to real-world function, they may also be based on item sizes and/or tags. Some items may exert an effect over all of your items with a certain tag, a certain size, a certain value etc.

### Item Effects
The core gameplay effects that an item can exert include:
- Damage (Strength)
- Healing (Stamina)
- Shielding (Warm-up)
- Health Regeneration (Recovery)
- Burning (Lactic Acid)
- Poisoning (Blood Toxicity)
- Slowing (Fatigue)
- Hasting (Speed)
- Freezing (Cramping)

### Enchantments
Encounters with diviners of the mystical arts, such as the Homeopath, will give the players opportunities to enhance their items with enchantments. 

### Legendary Items
In rare events, players will be given the opportunity to acquire Legendary items. These will be inspired by greats of the fitness industry, and will effectively ignore the base power scaling model. The player will not be given an opportunity to choose a Legendary item. When offered, it will be a blind random choice, or

## Balance Spreadsheet
Each item's expected power is a function of the item's tier, size and rarity.

Depending on the desired effect(s) of the item, a value will be assigned to the effect. The default value is 0, meaning that the item does not influence that vector. The sum of the effect weightings should be at least roughly equal to the expected power as part of the initial balancing pass. More work needs to be done on the weighting of each effect for the expected power scaling.

After the initial balance pass is complete, the plan is to design a simple ML model that will complete combat encounters with preset loadouts against enemies intended to appear at the currently tested stage. Telemetry data will be collected and used to determine the relative strength of each effect to achieve more fun levels of game balance. 

In an async online or PVE autobattler, it is desirable not to achieve 'perfect' balance. To a certain extent, the player should be motivated by a desire to 'break' the game, i.e achieving a build that exceeds the player's expected power level relative to their progress in a run.

The WIP game balance spreadsheet can be seen below:

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
    <iframe 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
        src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSQCZAWNd4zyNZzTHflVjFiLBVF5bFLW0G1lOaCLIW5tqnh3n0_WfXOSDOhxTW9-z5C8E4KNZsthS14/pubhtml?widget=true&headers=false">
    </iframe>
</div>
