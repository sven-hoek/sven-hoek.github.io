---
layout: post
title:  "Clustering with Fuzzy C-Means"
date:   2025-04-25 16:17:21 +0800
categories: blog
image: assets/img/fcm.png

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
Push the datapoints around with your mouse to form clusters and click the button to run the algorithm.
It will colorize them according to their cluster membership.

You may quickly realize that the algorithm has an obvious weakness:
If a cluster is stretched very long, some of its points may get assigned to a different cluster, even though there's a clear gap between them.
This is because the algorithm bases on the distances to the cluster centers but doesn't take into account the individual distances of datapoints to each other.

<link rel="stylesheet" href="{{ site.baseurl }}assets/css/styles.css" />

<div class="slider-container">
        <label for="numClustersSlider">Number of Clusters</label>
        <span id="numClustersValue">3</span>
        <input id="numClustersSlider" type="range" min="2" max="20" step="1" value="3" />
    </div>

<div class="slider-container">
    <label for="fuzzinessSlider">Fuzziness</label>
    <span id="fuzzinessValue">1.5</span>
    <input id="fuzzinessSlider" type="range" min="1.001" max="3.5" step="0.001" value="1.5" />
</div>

<div class="slider-container">
    <label for="maxIterationsSlider">Max Iterations</label>
    <span id="maxIterationsValue">30</span>
    <input id="maxIterationsSlider" type="range" min="1" max="200" step="1" value="30" />
</div>

<div class="slider-container">
    <label for="errorToleranceSlider">Error Tolerance</label>
    <span id="errorToleranceValue">0.001</span>
    <input id="errorToleranceSlider" type="range" min="0.0" max="0.1" step="0.0001" value="0.001" />
</div>

<div class="button-container">
    <button id="runAlgorithmButton">Run Algorithm</button>
</div>


<canvas id="fcmCanvas" style="touch-action:none;"></canvas>

<script src="{{ site.baseurl }}assets/js/interactive_animations/src/util.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/vector.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/input.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/environment.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/drawing.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/drawables/mouse_circle.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/drawables/constrained_point.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/drawables/soft_body.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/ndarray.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/colors.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/src/fcm.js"></script>
<script src="{{ site.baseurl }}assets/js/interactive_animations/fcm_example.js"></script>

The code can be found [here](https://github.com/sven-hoek/interactive_animations/blob/66e90aa47a9860b8ef503338fc08f0af174c2873/src/fcm.js).

Quite a while ago, I also wrote a Python version with standalone GUI, which you can find [here](https://github.com/sven-hoek/fcm_playground/).
