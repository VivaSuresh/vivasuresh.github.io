---
layout: page
title: Eigenfish Species
description: Using the eigenface algorithm for fish species identification
img: assets/img/goldfish.jpg
importance: 5
category: work
---

**Project Idea:**

Eigenfaces is a popular technique to identify unique faces that leverages Principal Component Analysis. For my work in FishSense, I was told to look into techinques for fish species identification. I thought that, maybe, Eigenfaces could be used to identify different species. Ultimately, it was a failure. But, I learned a lot in the process!

**Method:**
The way that Eigenfaces work is that it looks for the most important features of a training dataset of faces. Some faces will have longer noses, some will have darker hair, others will have higher cheekbones. Eigenfaces will take a certain number of the features and store them as "ghosts". Later, the "ghosts", or eigenfaces, can be used to reconstruct a given image. The scalar amount of these "ghost" faces will be unique and therefore let us know which unique face is being looked at. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/eigen_reconstruction.png" title="Eigen Reconstruction" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example of how "ghost" faces with certain scalar values can be used to reconstruct a face. Source: geeksforgeeks.org 
</div>

My idea was, if I could create a many "ghost" fishes of different species, maybe 30 or so "ghosts" per species, I could then attempt reconstruction with all these different groups of 30. For example, I would have 30 ghosts of goldfish, 30 of salmon, and 30 of great white sharks. These are the "eigenfish". Then, I would feed in a new image, and attempt to reconstruct these image using the goldfish eigenfish, and then the salmon eigenfish, and then the shark eigenfish. Whichever reconstruction was most similar to the original image would be the species I was looking for, because reconstructing a *goldfish* with *goldfish* ghosts is theoretically better than using *salmon* ghosts.

