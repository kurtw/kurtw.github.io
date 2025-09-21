---
title: "Blender"
excerpt: " Various projects using Blender"
header:
  teaser: /assets/images/solar_system.png
sidebar:
  - title: "Features"
    text: "Animation, python, 3D modeling"
share: false
toc: true
---

# Procedural Solar System
While learning a bit of Blender, I created a python script that generates a solar system with random planets, moons, and background stars (galaxies).
![SolarSys image](/assets/images/solar_system.png){: width="600px" style="display: block; float: left margin: auto" }

Each plant generated is chosen from 3 types: standard, rock, and water which then applies different materials based on the type. Every planet will be placed at a some orbit away from the star and has the possibility to have it's own moons. The background stars are just spheres with random colors applied.
![SolarSys_Blender image](/assets/images/solar_system_blender.png){: width="600px" style="display: block; float: left margin: auto" }

The script sets render settings, so after the system is generated, an animation of the planets and moons orbiting their parent can be made by selecting `Render > Render Animation` in the top bar. The output images can be used with the Video Sequencer to create a video of the animation. I like the result because it reminds me of Final Fantasy 7.
<video style="display:block; margin: auto;" width="600" controls autoplay loop>
    <source src="/assets/images/SolarSystemAnimation.mp4" type="video/mp4">
</video><br>

# Pumpkins
My kids at this time were **really** into Halloween, and especially pumpkins, so I decided to see if I could model some in Blender. It turns out getting the stem to look halfway decent isn't easy. I'm still not 100% satisfied with how it looks, but at some point enough is enough.
![Pumpkins image](/assets/images/pumpkins.png){: width="600px" style="display: block; float: left margin: auto" }