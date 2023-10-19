---
layout: page
title: GoPro Sync
description: Using an impulse to automatically synchronize two videos to create a stereo camera.
img: assets/img/gopro_background.jpg
importance: 2
category: work
giscus_comments: false
---

**Purpose of the Project:**

Stereo cameras are a great way of getting depth information from an environment, however commercial stereo cameras are expensive and often fail underwater. The Intel RealSense D455, possibly the greatest above-water stereo camera for its price, does not work underwater. The infrared projection it uses to create its own features to enhance its depth imaging fails underwater, due to red-light attenuation. The camera quality is even worse underwater due to ocean turbidity. And, flat port distortion becomes a big issue as well (see below). There are no dome ports for commercial stereo cameras. Therefore, it becomes necessary to use monocular cameras to simulate a stereocamera. 

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/flatport_distortion.png" title="Flat Port" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/domeport_distortion.png" title="Dome Port" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left is an example of flat port distortion. When the camera lens is flat, there is light refraction as described by Snell's law which causes image distortion. When a dome port is used instead, the image gets fixed, as seen on the right. 
</div>


GoPros are great for underwater use. There is precedent for using GoPros for underwater imaging, and there are lots of cheap dome ports to deal with flatport distortion designed for GoPros. So, how does one automatically synchronize two different GoPros? Doing it by hand will cause problems stemming from human error, which will throw off depth calculation. 

**Method:**

Instead of using video, I decided to use audio instead. As long as the camera itself has good audio/video sync, synchronizing two different videos using audio should work well. All a person needs to do is turn on both cameras and clap as loud as they can in front of both of them. This should create an impulse noise which can then be located using software. First thing is to extract audio data from each video. 

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/left_audio.png" title="Left Audio" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/right_audio.png" title="Right Audio" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The extracted audios from each GoPro.
</div>

As seen in the above charts, the impulse noise is VERY visible. However, just using the maximum value as the sychronization point of the two videos proved to be inaccurate. Thus, I needed to find conserved patterns within the two audio time series localized around the impulse point. To accomplish this, I used the stumpy library. Stumpy specializes in using matrix profiles to conduct time series analysis extremely quickly. The matrix profile is an indicator of the similarity of all the subsequences between two different time series. The lower the matrix profile value of a given subsequence, the more similar that subsequence is to another subsequence in the other time series. 


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/matrix_profile.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/left_subsequence.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/right_subsequence.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The lowest point of the matrix profile gives us the index of the most similar subsequences between the two time series.
</div>

From there, it was a simple matter of cutting the first few seconds of each video based on where the start of this subsequence was, and the videos are synchronized!