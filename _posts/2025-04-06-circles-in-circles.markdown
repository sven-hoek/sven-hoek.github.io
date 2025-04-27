---
layout: post
title:  "Circles in Circles in Gravity"
date:   2025-04-06 16:17:00 +0800
categories: blog

---

Quite simple and fast simulation of dynamics can be reached with Position Based Dynamics.
Instead of modeling forces and masses directly, the focus is on position constraints and projections.
Already with very simple rules, one can get impressively realistic-seeming simulations.
With enough self-avoiding points, it almost seems like a splashing liquid.

Touch the screen or move the mouse around to start and interact. Note that scrolling with a touchscreen requires to touch ouside the canvas area.
Elements either have a minimum distance (being pushed away from each other) or a maximum distance (being contained with one another).

<link rel="stylesheet" href="../../../../assets/css/styles.css" />

<canvas id="circlesInCirclesCanvas" style="touch-action:none;"></canvas>

<script src="../../../../assets/js/interactive_animations/src/util.js"></script>
<script src="../../../../assets/js/interactive_animations/src/vector.js"></script>
<script src="../../../../assets/js/interactive_animations/src/input.js"></script>
<script src="../../../../assets/js/interactive_animations/src/environment.js"></script>
<script src="../../../../assets/js/interactive_animations/src/drawing.js"></script>
<script src="../../../../assets/js/interactive_animations/src/drawables/chains.js"></script>
<script src="../../../../assets/js/interactive_animations/src/drawables/constrained_point.js"></script>
<script src="../../../../assets/js/interactive_animations/src/drawables/mouse_circle.js"></script>
<script src="../../../../assets/js/interactive_animations/circles_in_circles.js"></script>

The code can be found at [https://github.com/sven-hoek/interactive_animations/](https://github.com/sven-hoek/interactive_animations/).

Inspired by [Sublucid Geometry's blog post](https://zalo.github.io/blog/constraints/).
