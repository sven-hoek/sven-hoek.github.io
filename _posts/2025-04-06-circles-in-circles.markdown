---
layout: post
title:  "Circles in Circles in Gravity"
date:   2025-04-06 16:17:21 +0800
categories: blog

---

Touch the screen or move the mouse around to start and interact. Note that scrolling with a touchscreen requires to touch ouside the canvas area.
The simulation bases on simple distance constraints and Verlet integration.
Elements either have a minimum distance (being pushed away from each other) or a maximum distance (being contained with one another).

Inspired by [Sublucid Geometry's blog post](https://zalo.github.io/blog/constraints/), which has a little more info.

<canvas id="circlesInCirclesCanvas" style="touch-action:none;"></canvas>

<script src="../../../../assets/js/simple_physics_sim/src/util.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/vector.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/input.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/environment.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawing.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/chains.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/constrained_point.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/mouse_circle.js"></script>
<script src="../../../../assets/js/simple_physics_sim/circles_in_circles.js"></script>
