---
layout: page
title: Astronomical Spectroscopy Project
description: Class project for observational astrophysics course PHYS 164 at UCSD
img: assets/img/Flatfield_lab2.JPG
importance: 3
category: Class Projects
---

<div class="caption">
    <h3>Abstract</h3>
    In order to understand how astronomers use spectroscopy and spectrometry to measure physical
properties of stellar objects, we analyzed two datasets of spectral data. The first dataset was
obtained from a handheld spectrograph used to find the emission spectra of several elements.
The second dataset was from the KAST spectrometer, a detector in the Shane telescope of the
Lick Observatory. We use the handheld spectrograph dataset to develop an algorithm to find the
centroids of the emission spectrum in order to relate observed emission spectra to the pixel value
of the detection. Using the least squares linear fitting algorithm, we find a wavelength resolution
for both spectrographs with an error of σ = 7.686 pixels. Using these measurements and algorithms, we
characterize the chemical composition of several stars from their observed spectra to find their
spectral classification.
</div>

<h2>1 Introduction </h2>

To understand spectroscopy, one must understand what a spectrum is and where it comes from.
When a beam of light is diffracted, it separates into the wavelengths of light that make up that
beam. We call these wavelengths a spectrum as it is the spectrum of wavelengths that make up
the observed light from a source. These spectral lines tell us a lot about the physical properties of
the source of the light. From Kirchoff’s Laws of Spectra, we have three types of spectral
phenomena:

1. A continuous spectrum which is produced by a hot solid, liquid, or dense gas

2. An emission line spectrum which is produced by hot gas

3. An absorption spectrum which is produced by a cold gas lying in front of a continuous
spectrum.

Most astronomical bodies produce a continuous spectrum, which is approximated by the
spectrum produced from thermal radiation called blackbody radiation. This radiation relies only
on the temperature of the object, The spectral radiance (the power radiated per solid angle per
area per wavelength at wavelength λ at temperature T) is given by Planck’s Law:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq1_lab2.JPG" title="eq1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

When multiplied by the total solid angle of a sphere (4π), we get the equation for spectral
irradiance, the power radiated per area per wavelength of the astronomical body dependent on
temperature:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq2_lab2.JPG" title="eq2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

From this we can derive the body’s effective temperature from the maximum wavelength of light
emitted by the body through Wein’s displacement law:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq3_lab2.JPG" title="eq3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h2> 2 Observation and Data </h2>
<h4> 2.1 Collection of Data </h4>
To gather the data needed for this lab, we used two main devices to gather the data: a Ocean
Optics USB 2000 spectrometer and the blue arm KAST spectrograph, a spectrograph mounted
on the Shane telescope in the Lick Observatory.

The data from the Ocean Optics USB 2000 spectrometer was gathered by students in the winter
2020 UCSD observational astrophysics research lab due to the remote nature of the class the
quarter this lab was done in (winter 2021). The data collected by the USB 2000 consisted of
several frames of emission lines of four elements, Hydrogen, Mercury, Helium, and Neon, as
well as one arc lamp containing several elements.

The second dataset from the KAST Spectrograph was taken on October 26th, 2013 and accessed
by students for this lab on February 2nd, 2022. The dataset from the KAST Spectrograph
consists of bias frames, dome flatfield frames, and spectral frames that contain the continuous
spectrum of astronomical sources containing both emission and absorption lines.

<h4> 2.2 Instrumentation </h4>
<h5> 2.2.1 Ocean Optics USB 2000 Spectrometer </h5>

The Ocean Optics USB 2000 Spectrometer is a handheld spectrometer that focuses light from a
source then diffracts it onto an array of detectors. The technical layout of this spectrometer is
shown in Figure 2 in appendix 6.2. The USB 2000 used for this lab observes wavelengths
between 336 and 1027nm with a spectral resolution of ~0.4nm. The detector uses an array of
CCDs to count the intensity at each wavelength and converts the intensities to ADU with a
conversion ratio of 12 ADU per electron.

<h5> 2.2.2 KAST Spectrometer Blue Arm </h5>
The KAST Spectrograph is a camera mounted on the Shane Telescope which is located in the
Lick Observatory on Mount Hamilton, just east of San Jose, California. The KAST Spectrograph
is actually two spectrographs, one optimized for blue wavelengths and one optimized for red
wavelengths. They are mounted in such a way that both can be used at the same time if desired.
For the datasets for this experiment, we used the KAST Spectrograph’s blue arm as we are
looking at primarily blue wavelengths for emission and absorption spectra. A technical
schematic of the KAST double spectrograph is shown in figure 3 in appendix 6.3.

<h4> Displaying Data </h4>
To better represent the datasets used for this lab, we averaged all frames of each spectral
emission obtained from the USB2000. This allows us to analyze each element’s spectrum as a
singular entity instead of as the large number of files for each element’s spectral emissions. In
figure 4, we can see the spectral emissions of hydrogen, helium, and mercury.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig4_lab2.JPG" title="fig4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4: Spectral emission lines of hydrogen, mercury, and helium from the datasets recorded from the USB2000 handheld spectrometer
</div>

We can see the peaks of these datasets are excessively saturated, which is very apparent for
helium and hydrogen. Neon was the only spectra that did not exhibit these excessively saturated
peaks, and was not included in this figure because of it. This is an error that cannot be corrected
for, and it slightly offsets centroids at the saturated peaks which are found in this case using the
FWHM method.


<h2> 3 Data Reduction & Methods </h2>
<h4> 3.1 Centroiding Spectral lines </h4>
To convert the datasets from having a x-axis of pixel # to qualitative data with a x-axis of
wavelength, we need to calibrate the datasets from the spectrometer using the peak wavelengths
of known emission lines. To calibrate our spectral datasets, we must find the centroids of the
emission spectra. The centroids are not the pixel locations of highest intensity, but rather are the
pixel locations of the center of the intensity spikes of the spectrum. The centroids of the intensity
spikes are more useful than the peaks because they aren’t as reliant on spectral resolution and
because we don’t observe the highest intensity wavelengths at just one pixel.
To find the centroids of these spectral emission intensities for this lab, we use several methods to
calculate the centroids of each intensity spike. Firstly, set a threshold limit of two times the
minimum intensity value in each dataset as the limit that all peak intensities would be over.
Next, find the peaks of the emission spectra. Once the peaks have been found, we iterated over
the 30 pixels before and 30 pixels after each peak to find the points above half of the maximum
intensity of each spike. This is called the Full Width Half Maximum (FWHM) method. The
median value between the two half maximum points of each intensity spike was calculated as the
centroid.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig5_lab2.JPG" title="fig5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 5: Spectrum of Helium with the centroids of each emission line
</div>

<h4> 3.2 Converting Wavelength & Least Squares Linear Fitting </h4>

To convert from pixel number to wavelength, we need to fit the centroids of the datasets to the
actual observed emission intensities of elements. To perform this fit, we follow the Least Squares
Linear Fitting method (Least Squares fit). A linear equation takes the form y = m*x + b. To fit a
function linearly with the least squares method, we must find the minimum value of:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq4_lab2.JPG" title="eq4" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

The most likely values of m and c are present at the minimum possible Chi value. These values
can be found by solving:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq5_lab2.JPG" title="eq5" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

These are solved to have the form:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq6_lab2.JPG" title="eq6" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

These equations give us our two functions to find m and c from any x and y inputs. TO make
computations smoother for jupyterhub, we change the form of these equations to a singular
matrix equation that we use to perform our fit taking the form of:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq7_lab2.JPG" title="eq7" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Now, we can clearly see that by multiplying both sides of this equation by the inverse of the first
matrix, we will get this function in terms of m and c from our x and y inputs (corresponding to
centroid pixel and wavelength respectively). The error in this calculation is given in units of
pixels and the equations:


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq8_lab2.JPG" title="eq8" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Where σ is the variance in the system given by:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq9_lab2.JPG" title="eq9" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

This method allows us to identify the correlation between pixel number and wavelength so we
can convert our datasets from observed intensity per pixel to observed intensity per wavelength.

<h4> 3.3 Bias Subtraction and Flatfield Correction </h4>

The spectral data of astronomical sources from the KAST spectrograph must be reduced in order
to account for the bias noise and the individual pixel sensitivity in the detector. The first step in
this is very straightforward, we simply subtract the average of the bias frames from any other
frames we are using to account for the inherent noise in the system. The next main step is to
account for the pixel sensitivity. To do this, we need to use a flatfield correction, in which we
record several frames of a ‘flatfield’ which is a frame of a constant source with known intensity.
We normalize these flatfield frames by first taking the average of the flatfield frames, then
subtracting the bias, then dividing by the median of the flatfield minus the bias.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq10_lab2.JPG" title="eq10" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

This normalized flatfield frame tells us how sensitive each pixel is to light, so by scaling our
science frames by the normalized flatfield, we can better visualize the spectrum and can separate
out rows of detectors for analysis. The full flatfield and bias correction to each science frame is
equal to:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/eq11_lab2.JPG" title="eq11" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig6_lab2.JPG" title="fig6" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 6: Averaged and normalized flat field frames, with ADU count scales shown on the right.
</div>

We can see the need for the flatfield and bias correction here as one can clearly see the impact of
the pixel intensities causing a large dispersion in intensity values across the detector.

<h2> 4 Data Analysis & Modeling </h2>
<h4> 4.1 USB2000 Spectrometer Data </h4>
For the USB2000 spectrometer, we choose the Hydrogen arc lamp to calibrate the instrument,
and used the average of the 249 available hydrogen datasets for the highest accuracy
calculations.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig7_lab2.JPG" title="fig7" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 7: (top) Averaged hydrogen spectrum across wavelengths with centroids. (bottom) Least Squares fit for hydrogen files from USB2000.
</div>

The final fit parameters of the pixel number to wavelength conversion for the USB2000 using
the hydrogen arc lamp were:

𝑀 = 1. 125 ± 0. 021,
𝑐 =− 64. 820 ± 68. 573

Where our variance σ = 52. 932 which was used to calculate the uncertainty in these constants.

<h4> 4.2 KAST Sprectral Data </h4>
The chosen KAST files to analyze the spectral emissions were b160.fits (Fiege) and b156.fits
(BD+15233). To be able to analyze these astronomical frames, we must first calibrate the dataset
from pixels to wavelengths. The KAST file b100.fits is the spectral emissions of an arc lamp
recorded by the KAST spectrograph, so using the centroiding and least linear squares methods
used for the USB2000 data, we can translate the KAST pixels to wavelengths.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig8_lab2.JPG" title="fig8" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 8:  Shows the emission spectrum of an Hg, He, and Cd Arc Lamp recorded by the KAST Spectrograph
</div>

To make the fit quick and efficient, we used the top 8 most intense peaks of the arc lamp
emissions for our fit.
We have centroid pixel values of 639, 949, 1059, 1256, 1371, 1638, 1982. These correspond to
the wavelengths of 388.87, 404.66, 435.83, 467.82, 479.00, 508.58, 546.07 (nm). Using the least
squares linear fitting method, we get our fit parameters equal to:

𝑀 = 0. 1241 ± 0. 0023,
𝑐 = 303. 893 ± 9. 382

By multiplying the pixel values in each science frame by M and adding C to them, we can
convert our datasets from intensity per pixel to intensity per wavelength. This also gives us a
standard deviation of σ = 7. 686 pixels. Applying this fit to the pixel axis serves as conversion
from wavelength to pixels with this relative error.

<h2> 5 Discussion </h2>
Once we apply the wavelength calibration to the spectral frames we are analyzing, we get a
much clearer visualization of the data and can observe spectral features of the astronomical
sources.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig9_lab2.JPG" title="fig9" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 9: (Top) Shows the spectrum of b160.fits (Fiege 110). (Bottom) shows the spectrum of the b156.fits file (BD+15233)
</div>
From the spectral lines present in BD+15233, we find that the peak spectral emissions occur
around 300 ± 20𝑛𝑚. From this, we find using wein’s displacement law λ(max) = b/T_eff where
b=2898 um that the effective temperature for BD+15233 is approximately ~ 9660 ± 600𝐾. By
matching this calculated effective temperature to the temperature ranges of different spectral
classes shown in appendix 6.4, we see that BD+15 233 is of the spectral class A. However, upon
finding experimental results of the stellar classification of F0. The spectrum likely has a different
observed peak of spectrum here because we did not average all pixel columns of the detector to
get the clearest possible signal of our dataset.

From the spectral emissions of Fiege 110 (b160), we can see clearly that the peak of spectral
emissions is λ(max) < 110nm. From this, we have a minimum effective temperature for Fiege
using wein’s displacement law of T_eff(min) = 26350K . From this we see that Fiege is an
extremely hot star that must be an O type star because of its immense heat. Experimental
research confirms this assessment of Fiege 110’s spectral classification.

From these results, we can conclude that spectroscopy allowed us to be able to find effective
temperatures of stellar bodies from observing their emission spectrum and converting it to a
intensity vs wavelength plot. While our results were not entirely accurate of actual physical
observations, they were within the general region of the actual observed values of effecting
temperature and maximum intensity wavelength. This method allows us to effectively classify
stellar bodies from emission spectrums.


<h2> 6 Appendix </h2>
<h4> 6.1 Datasets </h4>
For the datalog of used KAST data visit Shane Data Repository, 2013/10/26
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig1_lab2.JPG" title="fig1" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<h4> 6.2 Ocean Optics USB 2000 Spectrometer </h4>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig2_lab2.JPG" title="fig2" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2:  Shows an internal layout of the USB 2000 Spectrometer with the following components:
    (1) Initial Aperture Lens, (2) Slit, (3) Optical Filter, (4) Collimating Mirror,
    (5) Diffraction Grating, (6) Focusing Mirror, (7) Lens to focus light for detectors,
    (8) Detectors. The incident and diffracted angles are shown, α, β respectively.
    These images were obtained from the USB 2000 Operating Instructions from Ocean Optics
</div>

<h4> 6.3 KAST Double Spectrograph </h4>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig3_lab4.JPG" title="fig3" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3: Shows the technical layout of the KAST double spectrograph
</div>

<h4> 6.4 Spectral Classes Table </h4>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/fig10_lab4.JPG" title="fig10" class="img-fluid rounded z-depth-1" %}
    </div>
</div>