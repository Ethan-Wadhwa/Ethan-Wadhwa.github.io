---
layout: page
title: Asteroid Tracking Project
description: Class project for observational astrophysics course PHYS 164 at UCSD
img: assets/img/NYSA_frame.JPG
importance: 4
category: Class Projects
---

<div class="caption">
    <h3>Abstract</h3>
    In this lab we took CCD images of asteroids using the Direct Imaging Camera on the Nickel 1-m
    Telescope at the Lick Observatory. We first developed algorithms to reduce our science frames
    by subtracting the bias and overscan area, multiplying by the gain obtained by flatfield images.
    We then developed an algorithm to identify and centroid star locations to accurately chart star
    locations on our CCD images. We then used the star locations from our images and queried the USNO-B1
    to find the actual right ascension, declination, and location of the stars in our frame to convert
    from pixels to standard coordinates. Once the objects in our frame had been converted to standard coordinates,
    we can relate the locations of the observed asteroid across frames to quantify the velocity of the asteroid.
</div>

<h2> 1 Introduction </h2>
In astronomy, the celestial sphere is a tool used to chart the locations of celestial objects in the
sky. The celestial sphere is a fixed projection of the sky onto a sphere with its equator along the
same axis as the Earths. By charting celestial objects on this sphere, astronomers label objects'
coordinates on the fixed sphere in terms of their right ascension (degrees to the left or right of the
celestial meridian) and declination (degrees above or below the celestial equator).
Star fields are the backgrounds of most astronomical images taken; they are the fields of visible
stars in the area behind a source being observed. Star fields are used for a much more important
task than being background noise behind a desired source; they allow astronomers to find the
exact location of a source on the celestial sphere. The star field in an image of a source can be
used to query databases containing the locations of known objects on the celestial sphere to
convert the image of a source from pixels to celestial coordinates. By doing this, astronomers can
accurately chart the motions of astronomical bodies by their movement along the celestial
sphere.


<h2> 2 Observing & Data </h2>

<h4> 2.1 Collecting Data </h4>
In this lab, we collected our CCD images using the Direct Imaging Camera on the Nickel 1-m
Telescope at the Lick Observatory. The telescope was accessed remotely by Physics 164 students
directed by Dr. Quinn Konopacky on February 28th, 2022 from the UCSD Observational
Astrophysics Lab Room. Several bias frames with the telescope shudder closed were taken, as
well as dome flatfield images taken in each of the five possible filters (UBVRI). The main data
used for this lab were CCD images taken by the physics 164 students of their chosen asteroids.
For our group, C/D, we chose to observe 44 Nysa, so three sets of five CCD images of 44 Nysa
were taken at different times throughout the observing period, two sets in the R filter and one set
taken in the V filter. The full list of data files used can be found in appendix 6.1.

<h4> 2.2 Catalog Databases </h4>
In this lab we rely on the USNO-B1 database to chart the predicted locations of stars in our
frames’ star fields. The USNO-B1 is a catalog of ~1 billion celestial objects derived from ~3.6
billion observations taken by the US Naval Observatory (USNO), all with magnitudes less than
V=21. This catalog also contains the approximate motion of the charted celestial objects to an
accuracy of approximately 0.2 arc seconds to the star’s locations in the year 2000. Movement of
each celestial body per year or ‘epoch’ has been calculated in this catalog as well, allowing us to
use the predicted locations of stars on our observing data (02/28/2022) to relate our CCD images
to actual celestial coordinates.

<h4> 2.3 Displaying Data </h4>
Let us take a closer look at the first and last 44 Nysa frames taken in the R band. To be able to
properly view our CCD images, we must first perform a bias subtraction, overscan removal, and
flatfield correction to display our images in their clearest form. Once this has been done, we can
observe several frames to view the movement of our chosen asteroid over time. As seen in figure
1 below, the chosen object (44 Nysa) clearly moves a significant distance within the time
between these two frames being taken. Additionally, in this image we can see the same star field
in the background of both frames, telling us we can use these stars to find the exact right
ascension and declination of 44 Nysa at the times of these frames.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig1_lab3.JPG" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 1: The first (left) and last (right) reduced 44 Nysa frames shown with gray color scale
    plotting to be able to better visualize objects present in the frame. The darker the points, the more
    intensity observed on those pixels. A bad column of detectors is present at roughly x=252,
    causing the inconsistency along that column. The largest dark point visible in both images is 44
    Nysa.
</div>

<h2> 3 Data Reduction and Methods </h2>
<h4> 3.1 Reduction of Astronomical Science Frames </h4>
The first step in reducing our data to be usable for our calculations is to remove the bias noise
and overscan region, and to correct for pixel sensitivity using dome flatfields. For this dataset,
we obtain a series of bias frames which can be averaged to use as a universal bias frame, and the
overscan region is given in the header of each file. To make this process simpler, we first remove
the bias and overscan from all frames before using the normalized flatfield frame to correct for
pixel sensitivity in our science frames. To remove the overscan and bias from our frames, we
subtract the averaged bias frame from our science frame then remove columns of the dataset in the
overscan region of the frame. To correct for the gain in the pixel sensors using the normalized flatfield,
we use a flatfield frame with bias and overscan removed and divide by the median value of said frame to obtain
the gain.

We can multiply our bias and overscan removed science frames by the pixel gain to obtain our fully
reduce science frames. The reduced frames can be seen in figure 1, with python functions used to
perform this reduction in appendix 6.3.1, 6.3.2.

<h4> 3.2 Identifying & Centroiding Star locations </h4>
To convert from x pixels and y pixels to standard coordinates we must first define which points
in our frame are stars. To do this, we locate potential stars by adding all pixels with
analog-digital units (ADU) counts above 1.5 times the median ADU count of the frame to a list.
To account for any pixels that detected low magnitude stars or that picked up light from any
other source, we reduce our list of every pixel location that has a high intensity to only the pixels
at the center of pixel clusters with high detected intensities. To do this, we search through a
square of a defined size around each high intensity pixel and if there are less than a specified
amount of other high intensity pixels in this area, we remove the pixel from our list. For pixels
that do have more than the limit of nearby bright pixels, we identify the approximate location of
the star to be at the highest ADU count pixel in the area. The code for this can be found at
appendix 6.3.3.

By identifying general locations of stars, we are able to reduce our centroiding algorithm to just
run in the areas of the general locations of the stars to find their exact centroids. We define the
areas to perform a centroiding function to be a 20 pixel by 20 pixel square centered at the star
locations identified on the frame. We then follow the centroiding algorithm for both x and y:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq1_lab3.JPG" title="eq1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Where x is the x pixel value at index i, y is the y pixel value at index i, and I is the ADU count
(intensity) at index i. The centroid values of each star give us the calculated center of each star in
x and y pixels with error calculated by:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq2_lab3.JPG" title="eq2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The centroiding function can be found at appendix 6.3.4, and is visualized in figure 2.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig2_lab3.JPG" title="fig2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2: Identified Stars with counts over each star in the first 44 Nysa frame taken at
    05:08:57.6, +20:58:51.4 at hour angle 21:00 on Feb 28, 2022. The brightest object marked with
    the number ‘2’ is 44 Nysa.
</div>

<h4> 3.3 Querying USNO-B1 Database to find Star Field Coordinates </h4>
Once we have our star locations in pixel coordinates, the next piece of information is the actual
right ascension and declination of the stars. To find the actual celestial coordinates of our stars,
we must first find our frames’ actual location on the celestial sphere. We find these coordinates
by querying the USNO-B1 database with the right ascension and declination of the center of our
frame obtained from the header of the data files. In order to access the USNO-B1 database, we
import astroquery.vizier into our code. Vizier allows us to find the exact right ascension and
declination of stars in the field of our image. We query Vizier with our frame coordinates,
magnitude limit, number of stars, field of view dimensions, and year of observation. Vizier
returns us a list of the celestial coordinates of any stars that meet our query condition. The code
for querying USNO-B1 can be found at appendix 6.3.5.

<h4> 3.4 Converting Frame Coordinates from Pixels to Standard Coordinates </h4>
Once we have obtained the pixel centroids of the stars in our frame and the queried actual right
ascension and declination of each star, we can perform a fit using a least squares approximation
of our data to convert our frame coordinates from pixels to celestial coordinates. To convert from
x and y pixel values to RA and DEC, we rely on the matrix equation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq3_lab3.JPG" title="eq3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

where x is our centroid objects’ pixel coordinate vector with the form (x , y , 1), X is our centroid
objects’ celestial coordinate vector with the form (RA, DEC, 1), and T is our transformation
matrix:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq4_lab3.JPG" title="eq4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The (f/p) ratio in this matrix is the lens in the telescope’s focal distance (f=16480 mm) and the
pixel size (p=0.0015mm). The six unknowns in this equation are our plate constants, with ai,j
referring to the scale, shear, and orientation and x0
, y0 being our offset in pixels. We can find the
values of the plate constants using least squares fitting. To find the plate constants, we must first
write out our x=TX equation for the X matrix of the actual Ra and Dec of our stars and x being
either the x pixel vector or y pixel vector. This gives us the matrix:
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq5_lab3.JPG" title="eq5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq6_lab3.JPG" title="eq6" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

And the version of this matrix for y has the an a vector of all y pixels and c=(a21 a22 y0)
Using these equations, we can calculate the plate constants by finding the least distance between
the points through the equation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq7_lab3.JPG" title="eq7" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

By minimizing χ^2 , we can multiply both sides of a=Bc by the transpose of B and the inverse of B
times transposed B to find our c vector values, giving us our plate constants.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq8_lab3.JPG" title="eq8" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

By performing this fit using both a vectors (both x and y pixel coordinate vectors) to find both c
vector values, we obtain our two sets of plate constants that we can plug back into matrix T. The
equation to convert from RA/DEC to pixel coordinates can be reversed to convert from pixel
values to ra/dec by multiplying both sides by the inverse of T to give us the equation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq9_lab3.JPG" title="eq9" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We plug each individual pixel coordinate into this equation with the coordinate vector of the
form x = [x pixel, y pixel, 1] to obtain our right ascension (α) and declination (δ) coordinates for
our centroid object locations with the form X = [α , δ, 1]. Once we have obtained the celestial
coordinates of our objects, it is a relatively straightforward conversion from celestial coordinates
to standard coordinates:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq10_11lab3.JPG" title="eq10_11" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Where X,Y are our standard coordinates, α_0 is the right ascension of the center of our frame and
δ_0 is the declination of the center of our frame. The code used to perform this conversion can be
found in appendix 6.3.6 and 6.3.7. This can be visualized in figure 3 shown in appendix 6.2.

<h2> 4 Calculations and Modeling </h2>
Now that we have our coordinates for our frames in both RA/DEC and standard coordinates, we
can examine two frames taken at different times to determine the change in RA and DEC of the
asteroid we chose to observe, 44 Nysa.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig3_lab3.JPG" title="fig3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3: (Left) Shows the first and last 44 Nysa frames taken plotted in standard coordinates (Right)
     Shows the first and last 44 Nysa frames taken plotted in celestial coordinates.
     Both plots have the earlier frame (taken at 6:58 pm PST) shown in blue and the later frame
     (taken at 8:43 pm PST) shown in red
</div>
The total time elapsed between the times these two frames were taken is about1 hour 45 minutes
or, for simplicity, 105 ± 5 minutes, with the error being therefore discrepancy in logged time of
observation and actual time of observation. The celestial coordinates of 44 Nysa in our first
frame are 𝑅𝐴_1 = 77.2537212 ± 0.0000017°, 𝐷𝐸𝐶_1 = 20.9839658 ± 0.0000004°. The celestial coordinates
of 44 Nysa in our second frame are 𝑅𝐴_2 = 77.2738905 ± 0.0000049°, 𝐷𝐸𝐶_2 = 20.9881811 ± 0.0000006°.
The errors in RA and DEC were calculated using equation (2). By finding the difference in the right
ascensions and declinations, we can find the total angle the asteroid has moved by using the
pythagorean theorem:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq12_lab3.JPG" title="eq12" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

We find the change in RA to be: ∆𝑅𝐴 = 0.0201693 ± 0.0000076° and the change in DEC
to be: ∆𝐷𝐸𝐶 = 0.0042153 ± 0.0000010°. These give us a total angle change of
θ ≈ 0.0206051 ± 0.0000092° with the error being given by error propagation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq13_lab3.JPG" title="eq13" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Converting this angle change into arcseconds using the equation 1𝑎𝑟𝑐𝑠𝑒𝑐 = , we have a 1°/3600
total angle change of 74.1784 ± 0.0331 arcseconds. Using the total change in time and total
change in angle, we can calculate the asteroid’s proper motion with the equation:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq14_lab3.JPG" title="eq14" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Here we have determined the proper motion of the asteroid 44 Nysa using our observations of
the asteroid.

<h2> 5 Discussion </h2>
Let us visualize the proper motion of 44 Nysa as calculated in the previous section.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig4_lab3.JPG" title="fig4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4: Plot of detected objects from the first frame analyzed with asteroid 44 Nysa labeled and
    its direction of proper motion shown
</div>

From figure 4, we are able to visualize the direction of motion of 44 Nysa across the celestial
sphere. The largest sources of errors in our measurements come mainly from the discrepancy in
our time measurements, the small error from the centroiding function, and the small error in the
pixel to celestial coordinate conversion. However, we are still able to calculate the proper motion
with an error of ~5% of our established measurement. More precise calculations of the proper
motion could be obtained from more measurements of 44 Nysa, each in 1 hour intervals on the
same night.

The proper motion of Nysa obtained from our observations does reveal several things about this
asteroid. First and foremost, the proper motion being of this magnitude tells us the object we are
observing must be relatively nearby as extremely distant objects’ proper motion is much smaller
than the proper motion obtained for Nysa. The other quantity the proper motion tells us is the
relative orbit of 44 Nysa in our solar system. The angle of 44 Nysa’s proper motion not being
zero relative to the earth tells us that it orbits along a different axis than Earth’s around the sun.
Improvements to this experiment would be measuring the parallax of the asteroid by taking
simultaneous measurements of the star on both sides of the continental United States. The
parallax of this asteroid would allow us to calculate the distance to it and thus using our proper
motion and distance calculate the transverse velocity of this stellar object. Another improvement
would be to create an algorithm to automatically match the queried star locations to the observed
star locations for more accurate conversion from pixel coordinates to celestial coordinates.
Overall, this lab yielded a measurement of the proper motion of 44 Nysa and several algorithms
useful to many different applications in astrometry.

<h2> 6 Appendix </h2>
<h4> 6.1 Data Files </h4>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.1_appendix_lab3.JPG" title="appendix1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h4> 6.2 Figure 5 - USNO-B1 Query Compared to Observed Frame </h4>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig6_lab3.JPG" title="fig5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3: (left) The first 44 Nysa frame’s centroid object locations converted to RA and DEC
    plotted against the actual star locations queried from USNO-B1. (right) The first 44 Nysa frame’s
    centroid object locations in standard coordinates plotted against the star locations queried from
    USNO-B1 converted into standard coordinates
</div>

<h4> 6.3 Main Coding Functions </h4>
<h5> 6.3.1 Bias Subtraction and Overscan Removal Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bias_overscan_remove_code.JPG" title="6.3.1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.2 Reduced Data Frame Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/reduced_sci_frame_code_lab3.JPG" title="6.3.2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.3 Star Locating Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/find_star_locs_code_lab3.JPG" title="6.3.3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.4 Centroiding Stars from Approx. Star Locationg Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/centroiding_func_lab3.JPG" title="6.3.4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.5 Querying from USNO-B1 Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/USNOB1_query_func_lab3.JPG" title="6.3.5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.6 Converting Centroids from Pixels to RA/DEC Function </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/convert_to_ra_dec_lab3.JPG" title="6.3.6" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h5> 6.3.7 Converting Centroids in RA/DEC to Standard Coordinates </h5>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/project_coords_lab3.JPG" title="6.3.7" class="img-fluid rounded z-depth-1" %}
    </div>
</div>