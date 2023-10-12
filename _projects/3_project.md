---
layout: page
title: Anomaly Detection in Seismic Data
description: Using machine learning to find anomalies in high dimensional data.
img: assets/img/spectrogram.jpg
importance: 2
category: work
giscus_comments: false
---

**Project Description:**

This project's purpose is to detect discords in Antarctic seismic data. There are lots of seismic readings taken from various devices around Antarctica, however the data itself comes in 8 channels of 64 x 313 matrices. That means that each snippet contains 160256 values. Therefore, it becomes necessary to reduce the dimensionality of the data in order to make successful comparisons between different snippets. 

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/normal_spectrogram.png" title="Good Spect" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/anomaly_spectrogram.png" title="Bad Spect" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left is an example of a nonanomalous spectrogram. On the right is a spectrogram with anomalies.
</div>

There are many known methods of dimensionality reduction that retain important features. PCA and other non-deep-learning techniques work very well with limited data, but because I had 1000 examples of nonanomalous data, I decided to use a 3 dimensional autoencoder. An autoencoder would be able to do better feature extraction than non-deep-learning techniques. 

<div class="row">
    <div class="col-sm text-center">
        {% include figure.html path="assets/img/autoencoder_model.png" title="autoencoder" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A summary of the autoencoder model that was used. 
</div>

In the end, the autencoder was able to detect **all 143 anomalies** present in the test data!
