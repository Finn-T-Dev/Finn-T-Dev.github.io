---
title: 'Gym-Themed Autobattler Prototype'
description: 'Devising system structure for gym-themed autobattler game inspired by The Bazaar & Balatro'
image:
    url: '/images/gym-autobattler/dumbbell.png'
    alt: 'Dumbbell placeholder'
platform: PC
stack: Unreal Engine 5 w/ NoesisGUI plugin
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
2. **Gym Simulator:** 
3. **Gym Empire:**

## Core Gameplay Loop
- Stage begins: Each encounter begins with taking stock of items in possession and looking ahead at the predetermined combat encounters ahead (events between designated combat encounters are hidden)
- Select an encounter from the 3 pseudorandomly generated events and resolve it for its effect (could be a merchant, selecting a buff if certain gameplay conditions have been met, or a miniboss etc)
- Acquire items and place them in the appropriate location (items with active effects go in the dumbbell rack, items with passive effects are automatically placed in the gym bag)
- Repeat until halfway through the stage, where a miniboss will be waiting. Select one of the minibosses and resolve the combat encounter.
- Continue to resolve encounters until the main boss of the stage. The victory condition for a stage is reducing the boss enemy's health bar to 0 before yours reaches 0 (ties are friendly).

## Balance Spreadsheet

Each item's expected power is a function of the item's tier and size.

Depending on the desired effect(s) of the item, a value will be assigned to the effect. The default value is 0, meaning that the item does not influence that vector. The sum of the effect weightings should be equal to the expected power as part of the initial balancing pass.

After the initial balance pass is complete, the plan is to devise a simple ML model that will complete combat encounters with preset loadouts against enemies intended to appear at the currently tested stage. Telemetry data will be used to determine the relative strength of each effect, and in turn, each item. 

In an async online or PVE autobattler, it is desirable not to achieve 'perfect' balance. To a certain extent, the player should be motivated by a desire to 'break' the game, i.e achieving a build that exceeds the power curve of the opponents

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
    <iframe 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
        src="https://docs.google.com/spreadsheets/d/e/2PACX-1vSQCZAWNd4zyNZzTHflVjFiLBVF5bFLW0G1lOaCLIW5tqnh3n0_WfXOSDOhxTW9-z5C8E4KNZsthS14/pubhtml?widget=true&headers=false">
    </iframe>
</div>
