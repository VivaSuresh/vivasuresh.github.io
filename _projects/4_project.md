---
layout: page
title: Semantic Segmentation for Autonomous Vehicles
description: Implementing multiple segmentation architectures and comparing the results
img: assets/img/semanticsegmentation.png
importance: 4
category: work
---

**Project Description**

Autonomous vehicles are an incredibly large industry, with an international market size estimated at USD 121.78 billion in 2022. Scene understanding is extremely important for autonomous driving safety and consistency. Semantic segmentation is one technique used for scene understanding. Cameras record roads, pedestrians, buildings, and other important objects, and each pixel within an image is assigned to a different object class. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/semanticsegmentation.png" title="Segmentation" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Each color represents a different object class. Note how pedestrians are all the same color, and how that is a different color from the road.
</div>

This is fundamentally a machine learning problem, as there is no known way to do this with non-deep-learning methods. However, even with deep learning, data becomes an issue. A lack of good data often limits deep learning models from performing well. Thus, the purpose of this project is to determine which segmentation models perform best given the same training and test data.

**Method**

After significant literature review, a few models stood out. FCN, U-Net, U-Net++, DeepLab, GCN, and SegNet were among those that were interesting. All of these models are filled to the brim with convolutional neural networks, which are able to extract data through a variety of different filters. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/segnet.png" title="segnet" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The SegNet architecture. Source: https://arxiv.org/abs/1511.00561
</div>

The chosen dataset was a subset of the CityScapes dataset. 2600 images were used for training, 300 for validation, and 500 for testing post-training. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/cityscapes_pair.png" title="segnet" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An example of the data taken from the CityScapes dataset. Source: https://www.kaggle.com/datasets/dansbecker/cityscapes-image-pairs
</div>

U-net, U-net++, and SegNet were tested to see which would perform the best. Standard data augmentation techniques were used, including mirroring, darkening/brightening, and blurring images to bolster the amount of training data. 

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/unet.png" title="U-Net" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/unet++.png" title="U-Net++" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left is the U-Net architecture. On the right is the U-Net++ architecture. Source: https://arxiv.org/abs/1807.10165v1
</div>

After a few hours of training, the following training and validation losses were presented by Tensorflow.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/unet_loss.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/unet++_loss.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/segnet_loss.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The training and validation loss of all different segmentation models tested.
</div>

Pixel Accuracy was the chosen metric for comparison, and the following pixel accuracies were calculated: 


<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/segmentation_results.png" title="Segmentation Results" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Per pixel accuracy of the different segmentation algorithms. 
</div>

The U-Net++ ended up having the best results, followed by U-Net and SegNet. However, at the same time, the U-Net++ had the most trainable parameters and also took the longest to train. So, it's definitely a tradeoff. However, because training only happens once and memory is not too much of a problem nowadays, U-Net++ is the segmentation algorithm to use!