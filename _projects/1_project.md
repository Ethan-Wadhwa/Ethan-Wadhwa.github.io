---
layout: page
title: Simon's Observatory
description: Test Equipment Design Projects
img: assets/img/sat_proj_pic.webp
importance: 1
category: work
related_publications:
---

During this project, I designed mounting equipment to mount a series of test equipment for the final phases of optical testing of the Small Aperature Telescope being assembled at UCSD. This telescope is studying the Cosmic Microwave Background (CMB) and has an extremely sensitive detector array as the CMB is very faint and had precise polarizations of which Simon's Observatory is attempting to quantify.

There were three main test systems I designed mounting equipment for:
1: A beam mapper which utilizes a small heat source and spinning 'chopper' blade to shine a thin beam at a modulated frequency to precisely test that each of the ~10,000 pixels on the detector array.
2: A Fourier Transform System (FTS) used to simulate light from an astronomical source to test the readout system as well as constrain the band widths and ensure that all necessary wavelengths can be observed.
3: A LN2 cold load to test the detector's bandwidth by observing a blackbody with emissions peaking at the same temperature as the Cosmic Microwave Background.

All three test systems needed to be mounted on top of a T-slot 'Cage' that could be locked in place around the telescope detector. By mounting the test equipment above the telescope in this fashion, we could precisely test the detector array in a controlled setting and shine the light sources directly downward onto the detector arrays.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SO_img_1.jpg" title="SO image 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SO_img_2.jpg" title="SO image 2" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SO_img_3.jpg" title="SO image 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Pictures of test equipment mounted above the aperture of the telescope as tested in lab. Left - FTS, Middle - LN2 Trap, Right - Beam Mapper
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


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
