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
for both spectrographs with an error of σ =. Using these measurements and algorithms, we
characterize the chemical composition of several stars from their observed spectra to find their
spectral classification.
</div>

<h2>1: Introduction </h2>

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


