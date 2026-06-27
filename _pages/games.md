---
title: Games
layout: single
permalink: /pages/games/
author_profile: true
show_date: false
toc: true
---
# Currently working on an unannouced multiplayer game.
Designing and building core gameplay systems.

## Related Skills and Tools
- Unreal Engine
    - Blueprints, Animation blueprints, Common UI, MVVM, Chaos Physics
- Multiplayer
- Optimization
- Debugging
- SVN

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