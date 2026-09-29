---
title: Games
layout: single
permalink: /pages/games/
author_profile: true
show_date: false
toc: true
---
# Stage Games: Unannounced UE5 Projects

Building core gameplay systems from prototype toward production in Unreal Engine 5 with C++ and Blueprint.

## Highlights

- Architected a networked interaction framework where clients scan and rank targets locally while the server re-validates each request before committing.
- Developed a data-driven building and placement system on voxel terrain, with a shared inventory moving resources between structures and vehicles.
- Integrated the Gameplay Ability System with configurable ability sets, and a gateway ability that routes interaction requests carrying custom target-data payloads.
- Modeled player status as a replicated GAS Attribute Set for hunger, stamina, and sickness, with data-table-driven states applied as gameplay effects.
- Designed an action-modifier system that resolves player and world state into one deterministic multiplier per outcome, applied at commit and designer-tunable without code.
- Designed one tool-and-knowledge gate serving both scavenging and staged dismantling, so the second mechanic reused the first system's gating and yield resolution instead of duplicating it.
- Built gameplay UI on Common UI and MVVM so C++ handles behavior and data flow while designers keep full control of layout and presentation.
- Migrated a phone and menu UI system onto Common UI with full gamepad, keyboard, and mouse navigation, leaving it in a state design and art could build on.
- Programmed gameplay-driven animation for Chaos Vehicles with Control Rig and Animation Blueprints, including FK crane articulation and hook and cable orientation solved at runtime.
- Stood up a dedicated automation test module, writing scoring, slot rules, and modifier math as world-free unit-tested logic alongside in-world functional tests.
- Authored the team's UI authoring, Gameplay Tag, content organization, and verification standards.

## Related Skills and Tools

- C++
- Unreal Engine
  * Blueprints, Gameplay Ability System (GAS), Common UI, MVVM, Enhanced Input, Replication, Chaos Physics, Control Rig, Animation Blueprints, Automation and Functional Testing
- Multiplayer
- Debugging
- SVN

## Examples of Work

### Interaction Targeting, Revisited

The priority-based selection I added on The Texas Chainsaw Massacre (below) solved the "used a toilet instead of a door" problem. On this project I built interaction from scratch and took the idea further, into a full scoring model.

Each candidate is scored from a base priority, a distance curve, an angle curve, a per-provider bias, a reticle bonus, and hysteresis that favors the current target so the prompt doesn't flicker between two close options. Line-of-sight and camera-cone checks filter candidates first, with a short grace period so a target doesn't drop the moment something briefly blocks it.

The client does all of this locally so prompts feel instant. When the player commits, the server re-resolves the target and re-validates the request before anything changes in the world. The scoring function doesn't depend on the world, so it's covered by unit tests rather than only by playtesting.

# The Texas Chainsaw Massacre
[![TCM image](/assets/images/TCM_image.png){: width="400px" style="display: flex; justify-content: center; margin: auto" }](https://www.txchainsawgame.com)
## Related Skills and Tools
- C++, C#
- Unreal Engine
    - Blueprints, Replication, Gameplay Ability System (GAS), Gauntlet, Unreal Motion Graphics (UMG)
- Multiplayer
- Optimization
- Debugging
- Perforce
- Rider and Visual Studio
- Consoles (Xbox and PlayStation)
- Jira

## Examples of Work
### Interaction System Update
#### Previous System
Selection was based on screen center distance. Meaning that an object would be selected for interaction based on how far it is from the center of the player's view. Overall, this selection method feels good to use because when a player rotates their camera towards an object they want to interact with it would be selected for interaction. The issue with this system is that it did not account for a few cases:

Type of object, object priority, and distance to the actual character on the screen
Without considering the above, scenarios like below start to arise.

##### Scenario A
1. A character is running towards a well with the intent to jump down it to avoid being hurt or killed.
2. Between the the well and the character, but slightly off to the side, is a health item.
3. Once the character passes the health item and the player (most likely) is rapidly pressing the interaction key, the character will stop and turn around to either take or use the health item because even though they are already past the item, the screen center to the item is now closer than the well.
4. The result is that the Family member will catch the player and hurt or kill them, which does not at all align with how the player thought the system should be working.

![SCD image](/assets/images/InteractionSystem_SCD.png){: width="250px" style="display: flex; justify-content: center; margin: auto" }

##### Scenario B
1. A character is running towards a door with the intent to slam through it to escape a Family member's advance.
2. Next to the door is a health item. The door and the health item have overlapping interaction areas.
3. When the player presses the interaction key, if the screen center is closer to the item the character will stop and pick up or use the item.
4. The result is that the Family member will catch the player and hurt or kill them, which does not at all align with how the player thought the system should be working.

![OLA image](/assets/images/InteractionSystem_OLA.png){: width="250px" style="display: flex; justify-content: center; margin: auto" }

#### New System
On top of all the original object selection criteria, the new system replaces screen center distance with proximity to the character on the screen and object priority. The intent was to "avoid using a toilet when the player really wanted to use a door".

The overhead for setup is slightly more than the original system because now each object that can be interacted with requires a priority level so that selection is picked from highest to lowest priority. If priority levels are the same, then proximity to the character as well as screen center distance comes into play to help make the decision.

The result mitigates scenarios like the ones previously mentioned, and also maintains the intuitive feel of the old system where if a player is looking at something they want to interaction, then they'll interact with that object.

# Fortnite
[![FN image](/assets/images/BtBites.png){: width="400px" style="display: flex; justify-content: center; margin: auto" }](https://www.blacktower.jp/blacktowerbites/)
## Related Skills and Tools
- Unreal Editor for Fortnite
- Verse
- Multiplayer
- Optimization
- Debugging
- Perforce, Unreal Revision Control
- VS Code
- Jira