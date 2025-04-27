---
layout: post
title:  "Fractal Tree"
date:   2025-04-27 16:17:21 +0800
categories: blog
image: assets/img/fractal_tree.png

---

One of the simplest fractals to create.
Playing around with the parameters is fun, though.
And with the right parameters, you can get something that doesn't resemble a tree at all anymore but has quite the beauty to it.

The rules to draw the trees are simple: At the end of each branch, create two more branches with a certain angle between them.

Move the mouse over the canvas to change branch length and angle.
Increase or decrease the depth to get simpler or more complex structures.
With the shortening factor, you can determine, how much shorter each branch gets, the higher up it is.
Values larger than 1.0 means the branches actually get longer towards the tree top and with a large enough angle, you'll get canvas-filling structures.

<link rel="stylesheet" href="/assets/css/styles.css" />

<div class="slider-container">
    <label for="depthSlider">Depth</label>
    <span id="depthValue">10</span>
    <input id="depthSlider" type="range" min="1" max="15" step="1" value="10" />
</div>

<div class="slider-container">
    <label for="shorteningFactorSlider">Shortening Factor</label>
    <span id="shorteningFactorValue">0.8</span>
    <input id="shorteningFactorSlider" type="range" min="0.1" max="1.5" step="0.05" value="0.8" />
</div>

<canvas id="fractalTreeCanvas" style="touch-action:none;"></canvas>

<script src="/assets/js/interactive_animations/src/util.js"></script>
<script src="/assets/js/interactive_animations/src/vector.js"></script>
<script src="/assets/js/interactive_animations/src/input.js"></script>
<script src="/assets/js/interactive_animations/src/environment.js"></script>
<script src="/assets/js/interactive_animations/src/drawing.js"></script>
<script src="/assets/js/interactive_animations/fractal_tree.js"></script>

The code is very simple, using recursion:
```js
function drawFractalTreeLine(start, length, branch_angle, current_angle, current_level, shortening_factor = 1.0) {
    if (current_level < 0) { return; }

    const end = start.add(Vector.fromPolar(length, current_angle));
    drawLine(start, end);

    drawFractalTreeLine(end, length * shortening_factor, branch_angle, current_angle + branch_angle, current_level - 1, shortening_factor);
    drawFractalTreeLine(end, length * shortening_factor, branch_angle, current_angle - branch_angle, current_level - 1, shortening_factor);
}
```

[According to Wikipedia](https://en.wikipedia.org/wiki/Fractal_canopy), there are structures in nature that resemble this fractal tree.
Obviously, there's trees, but also the pulmonary system, blood vessels, and more.
Also, when the branch-angle is 90 degrees (having your mouse horizonally in the center of the canvas), you'll get a [H tree](https://en.wikipedia.org/wiki/H_tree).
Not only does it look cool, it also seems to be useful in the design of integrated circuits or antennas.
