---
title: "Portal Plugin"
excerpt: "Multiplayer portal plugin for Lyra Starter Game"
header:
  teaser: /assets/images/PortalsActive.png
sidebar:
  - title: "Features"
    text: "Replication, gameplay ability system (GAS), game feature plugin, third-person"
share: false
---

This project was part of a test for a job interview. The project is a Game Feature plugin for the [Lyra Sample Game](https://dev.epicgames.com/documentation/en-us/unreal-engine/lyra-sample-game-in-unreal-engine) that adds
multiplayer portal mechanics. There are more in depth details about the project in the [repository](https://github.com/kurtw/PortalGame).
When I started this project I had never used Lyra before, so it was quite a learning journey.
It's not perfect, but it was a great way to get familiar with Lyra and Epic's best practices.
<video style="display:block; margin: auto;" width="600" controls autoplay loop>
    <source src="/assets/images/PortalMomentum.mp4" type="video/mp4">
</video><br>

The main feature of this plugin is the portal mechanic. While doing research I came across many
great first-person examples, but I thought it would be fun to try to do something from the third-person
perspective.

Some pain points for me while working on the plugin:

<u>The learning curve Lyra</u>

There is so much going on under the hood for Lyra (and Unreal Engine in general) that sometimes it's hard to know what to even look for when creating anything new or just troubleshooting in general. Thankfully there are a number of good resources out there.

Aside from source code, some notable resources I found are:\
[./X157](https://x157.github.io)\
[Lyra Dev Net discord](https://discord.gg/323cxWbx)\
[NanceDevDiaries](https://www.youtube.com/@nancedevdiaries)\
[Rakgul](https://www.youtube.com/@Rukgul)\
[Epic Dev Community](https://dev.epicgames.com/community/)

<u>Getting the rendered view from each portal to look good from the third-person perspective</u>

In the current state, it's too magnified and offset.

<video style="display:block; margin: auto;" width="600" controls>
    <!-- <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/PortalView_current.mov" type="video/mp4">
</video><br> -->
    <source src="/assets/images/PortalView_current.mp4" type="video/mp4">
</video><br>

<u>Niagara effect flickering</u>

At least on macOS, the Niagara effects do not play well once the portals are spawned. The effects have intense
flickering. My current solution is to disable rendering for the Niagara system attched to the B_WeaponSpawner
and BP_ExperienceList3D.
<video style="display:block; margin: auto;" width="600" controls>
    <!-- <source src="https://github.com/kurtw/kurtw.github.io/raw/main/assets/images/NiagaraFlicker.mov" type="video/mp4">
</video><br> -->
    <source src="/assets/images/NiagaraFlicker.mp4" type="video/mp4">
</video><br>