---
layout: post
title:  "Clustering with Fuzzy C-Means"
date:   2025-04-25 16:17:21 +0800
categories: blog

---

Imagine, you may have collected data about your customers, such as age, height, body weight, earlobe area, egg consumption.
The data definitely was collected with the consent of your users and now you want to figure out if your users can be grouped into a certain number of groups, so you can provide better service to each of them.
Most likely, some users won't fall into exactly one group, so you'd also like to quantify each user's partial membership in each group.

One common algorithm to cluster such data is [K-means Clustering](https://en.wikipedia.org/wiki/K-means_clustering).
However, it will assign each data point to exactly one group.
Very similar is the [Fuzzy C-Means algorithm](https://en.wikipedia.org/wiki/Fuzzy_clustering), where you have a hyper-parameter, determining how sharp the group boundaries will be.
There are various methods to find out, which [number of clusters](https://en.wikipedia.org/wiki/Determining_the_number_of_clusters_in_a_data_set) may best describe your data but let's say, you already know how many clusters there are in your customer base, e.g. `k` clusters.

The algorithm is rather simple:
1. To each data point `x`, initialize `k` values of cluster affiliations randomly
1. Repeat the following steps until you reach the set limit of iterations or the change in cluster affilitations falls below a set error threshold
    1. Calculate the centroid of each cluster by calculating the weighted sum of each datapoint, using the affilitation to the current cluster as weight.
    1. Update each datapoint's affilitation to the cluster by calculating their distance to the cluster centroid

The algorithm will work with any n-dimensional data but in 2D, it's very easy to visualize. Below you can set the parameters of the algorithm.
Push the datapoints around with your mouse and click the button to run the algorithm and colorize them according to their cluster membership.

You will realize that the algorithm has an obvious weakness:
If a cluster is stretched very long, some of its points may get assigned to a different cluster, even though there's a clear gap between them.

<style>
  #runAlgorithmButton {
    font-size: 16px;
    padding: 15px 10px;
    border-radius: 5px;
    margin-bottom: 10px;
  }
</style>

<div class="slider-container">
    <input id="numClustersSlider" type="range" min="2" max="20" step="1" value="3" />
    <label for="numClustersSlider"><span id="numClustersValue">3</span> Number of Clusters</label>
</div>

<div class="slider-container">
    <input id="fuzzinessSlider" type="range" min="1.001" max="3.5" step="0.001" value="1.5" />
    <label for="fuzzinessSlider"><span id="fuzzinessValue">1.5</span> Fuzziness (the closer to 1, the sharper the boundaries)</label>
</div>

<div class="slider-container">
    <input id="maxIterationsSlider" type="range" min="1" max="200" step="1" value="30" />
    <label for="maxIterationsSlider"><span id="maxIterationsValue">30</span> Max Iterations</label>
</div>

<div class="slider-container">
    <input id="errorToleranceSlider" type="range" min="0.0" max="0.1" step="0.0001" value="0.001" />
    <label for="errorToleranceSlider"><span id="errorToleranceValue">0.001</span> Error Tolerance</label>
</div>

<div class="button-container">
    <button id="runAlgorithmButton">Run Algorithm</button>
</div>


<canvas id="fcmCanvas" style="touch-action:none;"></canvas>

<script src="../../../../assets/js/simple_physics_sim/src/util.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/vector.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/input.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/environment.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawing.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/mouse_circle.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/constrained_point.js"></script>
<script src="../../../../assets/js/simple_physics_sim/src/drawables/soft_body.js"></script>
<script src="../../../../assets/js/ndarray.js"></script>
<script src="../../../../assets/js/colors.js"></script>
<script src="../../../../assets/js/fcm.js"></script>
<script src="../../../../assets/js/fcm_example.js"></script>
