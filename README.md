# Larceny
Set in North America, Larceny is a cooperative first person shooter heist game inspired by Overkill’s Payday 2.  The game aims to separate itself in the market through its levelling system (inspired by Skyrim), parkour mechanics, unique levels integrated with distinctive equipment, black market, and notoriety. The game will be built on Epic’s Unreal Engine 4 with an early access planned for mid 2019 at $20 and the final release in mid 2020 for $30. The game will be marketed via IndieDB, Gamebanana, Reddit, Discord, and Steam.

# System Overview

The system works by using structure called &quot;Weapon Data&quot; that contains all the variables necessary to setup, load, and use a weapon in the game. This structure is put into a map that allows the weapon to have a name associated with the structure. All of the management of Ammo, Animations, Firing Modes, and ADS is handled backend by the system.

# Exporting for UE4

1. Put **everything** in your scene under one parent (a dummy works fine).
2. Put the dummy in the back of your weapon mesh. This controls where the weapon delay (occurs when you move the mouse) rotates from. Personally, I find that rotation from the back looks the best.
3. Split up pump action reload animations according to the guide given under &quot;Setting up your Weapon&quot;

# Getting Started

In order to get started, navigate to Content/Larceny/Core/Characters and open &quot;Char\_Base.&quot; Locate the variable called &quot;Static\_Weapon\_Data&quot; in the Variables section (bottom left). Click on the variable and look to the right of your screen. In here, you will be able to add and remove weapons, set their data, and give them names.

1. Click on the add element button to add a new weapon
2. Hover over each variable to get a tooltip of what they do and what value to give them. For a detailed overview of how to setup your weapon, please check the next section.
3. Set your weapon to be the preview weapon by setting the &quot;Preview Weapon Name&quot; variable to the name of your weapon
4. Add your weapon to the weapon list in the variables panel. The index of the item (starting from 1 and going up) will be the key you use to select it in game.

# Setting up your Weapon

Here is a detailed overview of each variable in each weapon entry. Note that examples are given for two rifles and a shotgun. (KAC, G3SG1, and R870)

Mesh: Put your skeletal mesh here. This is the mesh that represents your weapon and will be put in front of the camera in-game.

Weapon Type: The weapon type decides the animations that will be used and animation locking. Currently, only Rifle and Pump action are supported. Rifle for the time being is very general purpose.

Relative Transform: If your mesh isn&#39;t lined up with the camera in-game, use the relative transform to adjust rotation, location, and scale to make it align correctly. You can do this by setting the Preview Weapon Name to be the name of the weapon you are currently working on. Then go to the viewport (tab in the middle of the screen) and change the values of the relative transform until it aligns correctly.

Fire Rate: This value determines how fast the weapon should be fired. Specifically, 1 second is divided by the number value of the fire rate variable. As a result, a fire rate of 5 would mean the weapon would fire every 0.2 seconds (1  second / 5). For pump action, this controls the multiplier of the animation speed instead.

Max Ammo: Controls the maximum amount of ammo the weapon can hold.

Firing Modes: An array of all the firing modes that the weapon supports. The first firing mode is always the default and then the others are used when switched to (X). It currently does not support an animation for switching modes (coming in the next version).

Animations: This section is loaded as it varies from weapon type to weapon type. A full run down of each animation for each **supported** type is given below. This will be updated as more types are added.

## General

The &quot;Locks Anim&quot; Boolean controls whether the animation blocks other animations from running. The &quot;Lock Time&quot; controls how long this is for lock is for. To add an animation, add a new element and type of the name of the animation.

## Rifle

Draw – Only allows for animation and runs when the animation is drawn.

Idle – Only supports one animations and runs when no other animations are running

Reload – Only supports one animation and runs when the weapon is reloaded and there is ammo remaining

Reload\_Empty – Only supports one animation and runs when the weapon is reloaded and there is no ammo remaining

Fire – Supports multiple animations that will be iterated through as the weapon is fired.

## Pump

Draw – Only allows for animation and runs when the animation is drawn.

Idle – Only supports one animations and runs when no other animations are running

Reload – **Requires**** 4 animations**. The first animation is the start of the reload. The second animations is the repeating part of the animation (putting the shell in). The second and third animation are the ending animation with or without pump (without is 3 and with is 4).

Fire – Supports multiple animations that will be iterated through as the weapon is fired.

Pump – Supports one animation and runs when the weapon needs to be pumped.

## Recoil

X – Controls the amount of recoil on the x-axis (left/right). This value is randomized (between 0 and given value) to provide some variation.

Y – Controls the amount of recoil n the y-axis (up/down). This value is slightly randomized by 0.1 to provide variation.

## ADS Location

This is the by far the most annoying item to setup. Currently, poses are not supported and a position must be set for the weapon when in ADS mode. Here is a step by step guide to setting up ADS.

1. Go to &quot;Construction Script&quot; which is found on the bottom panel on the left near the top. Move the execute wire (the big white one) from &quot;Set Relative Location&quot; on the node right after &quot;Construction Script&quot; to the &quot;Set Relative Transform&quot; at the bottom by dragging the white triangle on the right of the first node to the white triangle on the left of the second node.
2. Move to the &quot;viewport&quot; by pressing the tab near the top left of your window. Adjust the ADS location of your object until it appears to be centered on your screen.
3. Test by pressing play in the viewport and pressing right click to toggle ADS.
4. Die of AIDs because that&#39;s how fucking annoying this system is right now to setup.


