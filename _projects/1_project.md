---
layout: page
title: Autonomous Underwater Laser Detection
description: Automatically detecting a laser dot underwater.
img: assets/img/laser_project_background.jpg
importance: 1
category: work
related_publications:
---

<!-- Every project has a beautiful feature showcase page.
It's easy to include images in a flexible 3-column grid format.
Make your photos 1/3, 2/3, or full width. -->

**Motivating Automatic Underwater Laser Detection:**

State of the art techniques for measuring fish length involve capturing fish and measuring them above water or training divers to 'eyeball' fish lengths. Both methods are extremely resource intensive and the latter is inaccurate. However, using a rigidly attached laser on a camera, it is possible to get the distance that a laser dot hits.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/laser_1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/laser_2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/laser_3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The laser dot move towards the vanishing point as the object it hits gets farther away.
</div>

The FishSense research team was able to implement an algorithm that can take a laser dot in an image and, after thorough calibration, get the depth at that point. Then, when pointed at a fish that is perpendicular length-wise to the camera, as seen below, trigonometry can be used to get fish length. The method isn't perfect, but it is far superior to currently used techniques. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/perpendicular_fish.png" title="Example Fish" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example of how trigonometry can be used to calculate the length of a fish, given that it is perpendicular to the camera.
</div>

The problem is that it takes multiple seconds to label each laser. Each deployment returned thousands of images of fish whose lengths needed to be measured. Thus, an autonomous system to detect laser dots is necessary.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
