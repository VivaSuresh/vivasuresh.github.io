---
layout: page
title: Eigenfish Species
description: Using the eigenface algorithm for fish species identification
img: assets/img/goldfish.jpg
importance: 5
category: work
---

**Project Idea:**

Eigenfaces is a popular technique to identify unique faces that leverages Principal Component Analysis. For my work in FishSense, I was told to look into techinques for fish species identification. I thought that, maybe, Eigenfaces could be used to identify different species. Ultimately, it was a failure. But, I learned a lot in the process! Please take a look at my code in the repositories tab above!

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

**Method:**

First things first, Eigenfaces only works with grayscale images. However, converting fish images into grayscale causes loss of important features, as color helps a LOT with species identification. In order to combat this, I decided that I would run PCA 3 times, on each color channel (red, green, and blue color channels). Thus, I would have 3 groups of 30 different eigenfish per species. Then, reconstruction would happen on each color channel separately, and the reconstructed images would be combined together to form an RGB image. Below are a few examples of golfish eigenfish.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eigenfish_1.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eigenfish_2.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eigenfish_3.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    These are examples of the "ghosts" or eigenfish for goldfish.
</div>

Ultimately, however, I realized that there was just not enough data for this to work. And, if I was able to get a few hundred images of fish, it would be better to use a Mask-RCNN or a YOLO network for species identification, as deep learning would show better results. YOLO networks are the current state-of-the-art for underwater species identification. On top of that, red light attenuation in water causes colors of fish to change dramatically underwater based on the distance from the camera, and PCA is just not adaptable enough.