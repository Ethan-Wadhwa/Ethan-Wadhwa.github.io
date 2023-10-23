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

There were three main test systems I designed mounting equipment for.
1st, a beam mapper which utilizes a small heat source and spinning 'chopper' blade to shine a thin beam at a modulated frequency to precisely test that each of the ~10,000 pixels on the detector array.
2nd, a Fourier Transform System (FTS) used to simulate light from an astronomical source to test the readout system as well as constrain the band widths and ensure that all necessary wavelengths can be observed.
3rd, a LN2 cold load to test the detector's bandwidth by observing a blackbody with emissions peaking at the same temperature as the Cosmic Microwave Background.

All three test systems needed to be mounted on top of a T-slot 'Cage' that could be locked in place around the telescope detector. By mounting the test equipment above the telescope in this fashion, we could precisely test the detector array in a controlled setting and shine the light sources directly downward onto the detector arrays.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SO_img_1.jpg" title="SO image 1" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/SO_img_3.jpg" title="SO image 3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Test equipment mounted above the telescope as tested in lab. Left - FTS, Right - Beam Mapper.
</div>

The work I did designing the mounts for the test equipment involved iterating and simulating a series of designs using SOLIDWORKs. For the LN2 trap and Beam Mapper, the mounting systems were made of several custom designed aluminum plates and a series of T-slot beams to keep the weight of the test equipment distributed evenly to keep them stable and areas below the suspended load safe during the testing process.
For for FTS, I had to design a hanging cage that could move laterally as well as have an adjustable mirror to specifically adjust the outgoing angle of the light from the FTS.

With the FTS, due to the complexity of the simulation and relative light weight of the system (FTS  ~ 70lbs, cage ~60 lbs), the design was based more around functionality and ability to move various components without any electronics as the FTS was to heavy for the Beam Mapper linear actuator system.
The design is made up of several main parts, the linear stages that mounted to the top of the T-slot beams, the cage that suspends the FTS below the beams and above the telescope, a mount to keep the light source in front of the FTS entrance but around the chopper blade, and an adjustable mirror to change the angle which the FTS outputs the light into the telescope.
This resulted in the design seen below, which was the implemented after a series of iterations due to a failed magnet in the FTS preventing a simpler configuration.
The mirror and hinge were the two relatively simple custom pieces designed for the FTS mounting, with all other parts being ordered from McMaster Carr and built by me at UCSD.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fts_cage_sw_1.jpg" title="FTS cage design" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fts_mirror_sw_1.jpg" title="FTS adjustable mirror closeup" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    FTS Solidworks final design (left) and closeup of the FTS exit aperture and adjustable mirror jig (right)
</div>

For the Beam Mapper, I had two tasks as the linear actuator system had already been designed and a graduate student was working on the control system for it. My job was to create a simple system to mount the Beam Mapper to the T-slot cage to suspend it above the telescope and to create a simple cable management system to run wires to the necessary parts of the beam mapping system.
With this design, I had two main support beams with a custom plate to attach the linear actuators to the support beams. For the cable management system, I found some cable carriers and designed custom mounting pieces to connect them to the linear actuator and route the cables simply and efficiently across the whole range of motion of the beam mapper.

Below are images of the beam mapper design as well as the results of one of the solidworks simulations I ran of the custom plate to verify it met the safety criteria of usage in this system.

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/beam_mapper_sw_2.jpg" title="Beam Mapper Mount" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/beam_mapper_sw_1.jpg" title="With BM attached" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/beam_mapper_cable_management.jpg" title="Cable Management" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/beam_mapper_custom_sim.jpg" title="Beam Mapper Sim" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

