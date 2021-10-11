Data Products
===============

Continuum
#########

Image validation
****************
The continuum images were individually validated for every beam. In order to do this, a set of metrics was defined which inform on different aspects of image quality. The starting point of the validation are the residual images obtained after cleaning the continuum images. The validation aims at checking to what extent these images only contain Gaussian noise. The premise being that any significant deviation from this indicates issues with the calibration and/or the reduction of the data.

The following parameters were derived for each residual image.

* σ_in: Noise in inner half degree of the image, determined in a robust way from the residual image using the median of the absolute values.
* σ_out Noise at the edge of the residual image, more than a degree from the centre  determined in a robust way from the residual image using the median of the absolute values. This value is taken as a reasonable measure of the expected noise.
* R=σ_in/σ_out: A measure of the strength of artifacts left in the centre of the residual image.
* Ex-2:  Area, in units of beam area, with values below 2 σ_out in the inner 0.5 degree of the residual image, in excess of what expected from a purely Gaussian distribution. For perfect noise Ex-2 = 0.
* MaxNeg: the level, in units of σ_out, at which the area covered by pixels with values below this level is 10 beams. The expected value is -3.2. More negative values indicate significant negative calibration residuals.

Note that we did not use the equivalents of the parameters Ex-2 and MaxNeg based on positive deviations from Gaussianity (Ex+2 and MaxPos). This is because many residual images have weak, positive residuals due to insufficient cleaning which would then dominate the validation.

Visual examination of a large set of images was undertaken to define the numerical criteria that would catch significant image artifacts, as used above. The main types of image artifacts due to errors in the selfcalibration as well as strong direction-dependent errors for which the calibration pipeline did not attempt to correct. The criteria were set so that the large majority of images which were visually assessed as good would pass while only a small fraction of images that were visually assessed as bad would be classified as good.

The final criteria used to reject images are:
* R > 1.225. This criterion catches stripes due to errors in the amplitude calibration.
* R > 1.15, MaxNeg < -4.5 and Ex-2>400. This criterion catches general image artifacts and deviations from Gaussianity in the residual image.

Two additional criteria were set based on survey specifications:
* σ_in or σ_out  > 60 microJy/beam. In this case the noise of the image does not meet the  minimum requirement to be considered survey quality and valid.
* The minor axis of the restoring beam is > 15 arcsec. This occurs when both dishes RTC and RTD are missing from an observation. In this case, the required angular resolution of the survey is not met.

Flux scale & astrometry
***********************
For checking the consistency of the flux scale two beams of an observation of a field in the Perseus-Pisces region centered on RA(J2000) = 01h55m and Dec(J2000) = 33d56’ which was observed ten times between September 2019 and January 2020 were examined. The automatic source finder PyBDSF (also used in the Apercal pipeline) was used to find and determine source fluxes, positions and sizes and compared these from observation to observation. We restricted the comparison to sources that are less than 35” in size and have fluxes above 3 mJy (100 times the typical rms noise)  and agree in position to within 3 arcsecs to ensure that the sources used for comparison are indeed identical and have been included in the clean masks.

The overall consistency is very good with a mean of 1.014 and an rms of 4% . If one excludes the two most discrepant observations (ObsID 191207035 and 191227014) the rms decreases to 2%. Table 1 provides the flux ratio of 10 observations relative to the last observation made on 06.01.2020 (ObsID 200106010)

.. csv-table:: Table 1
  :align: center
  :header: "ObsID", "Median Flux Ratio"
  :widths: 20, 20

  190919049, 0.9982
  191207035, 0.9311
  191223022,  1.0041
  191225015,  1.0116
  191227014,  1.1069
  191229014,  1.0185
  191231013,  1.0062
  200102012,  1.0446
  200104011,  1.0222
  200106010,  1.0000

An example of two observations (ObsID 200106010 and 190909049, observed at 06.01.2020 and 09.09.2019 respectively) compared to one another is shown in Figure 1. Plotted is the relative difference in flux versus the flux in the 06.01.2020 observation.

.. figure:: images/flux_cmp_1.png
  :align: center
  :width: 400
  :alt: Relative flux error

  Figure 1. Relative flux difference between the sources in a mosaic of ObsID 200106010 and a mosaic of ObsID 190909049 as a function of their flux measured in ObsID 200106010.

To assess the agreement with the NVSS we made mosaics of the full field of view (40 beams) of all observations using the measured shapes of the 40 beams. The reason for using mosaics rather than individual beams was to have a large enough number of sources for the comparison as in an individual beam there usually are only of order a dozen that are bright enough. The mosaicing routine takes into account shapes of the beams made with the phased array feeds as determined from drift scans across Cygnus A (see the section on Primary beam response: Drift scan method) and corrects for the presence of correlated noise in adjacent beams. The mosaics were made with a resolution of 28" x 28". We ran PyBDSF on the mosaics to produce a source catalog and compared sources in this catalogue with the sources in the NVSS source catalog extracted from VizieR. For the comparison we restricted ourselves to sources that agree in position to within 4", are less than 28.5" in size and stronger than 3 mJy in the Apertif mosaic.

Table 2 captures the comparison of the individual mosaics with the NVSS. For each ObsID the median flux ratio NVSS / Apertif is given. On average the Apertif flux scale is 3% above the NVSS flux scale for these mosaics with an rms of 4%. If the two most discrepant ObsIDs are omitted (191207035 and 191227014) the rms reduces to 2%. Figure 2 illustrates the agreement between the Apertif and NVSS flux scale for ObsID 200102012. Since the observing frequency of the mosaic is 1360 MHz as opposed to the 1400 MHz of NVSS ~2% of the flux difference can be accounted for by spectral index effects (assuming an average spectral index of -0.7) which were not taken into account.

.. csv-table:: Table 2
  :align: center
  :header: "ObsID", "Median Flux Ratio"
  :widths: 20, 20

  190919049, 0.943
  191207035, 0.894
  191223022, 0.962
  191225015, 0.969
  191227014, 1.083
  191229014, 0.980
  191231013, 0.974
  200102012, 1.004
  200104011, 0.976
  200106010, 0.964

A flux scale comparison using the beam shapes determined from a direct comparison of the DR1 observations with NVSS using a Gaussian process regression technique provides a better picture as all DR1 data are used rather than just one field.

.. figure:: images/flux_cmp_2.png
  :align: center
  :width: 400
  :alt: Relative flux error

  Figure 2. Relative flux difference of sources in the NVSS catalogue and sources measured in an aperitif mosaic of ObsID 200102012 as a function of the flux of the sources in the NVSS catalogue

This is described in "Characterization of the primary beams" and yields a current estimate of the flux scale of Apertif as compared to NVSS. From this comparison the Apertif fluxes are on average 9% higher than those of NVSS, accounting for a nominal spectral index of the sources of -0.7.

Since we had to match sources in Apertif and NVSS for the source comparison we also obtained information on the agreement between the Apertif and NVSS astrometry. Figure 3 shows the positional differences for sources in the mosaic of ObsID 200102012 and the NVSS catalogue. The agreement is very good with mean offsets of 0.05 +/- 0.2  arcsec in RA and -0.05 +/- 0.2  arcsec in Dec.

.. figure:: images/flux_cmp_3.png
  :align: center
  :width: 400
  :alt: Relative flux error

  Figure 3. Position difference between the sources in the NVSS catalogue and the sources detected in the mosaic of ObsID 200102012.

Polarization
#############

Validation of polarisation cubes/images
***************************************

Two types of polarisation products are generated by the pipeline. The first one being cubes of Stokes Q and U of 24 images each covering a bandwidth of 150 MHz resulting in a frequency resolution of 6.25 MHz. The second products are Stokes V images generated from the whole combined bandwidth of 150 MHz.

Due to the different characteristics of these products two different sets of metrics were used to validate their quality. These metrics are very similar to the ones used for the continuum validation, but needed to be adjusted due to the following reasons:

# Due to the physical nature of Stokes Q, U and V emission in the cubes can be a positive or negative quantity while it can only be positive in Stokes I.
# Image artefacts are mostly influenced by the instrumental leakage characteristics of the primary beam in combination with direction dependent effects. This means that the strongest artefacts often appear for sources far away from the beam centres where the instrumental leakage is higher.
# For Stokes Q and U even faint artefacts in individual images can stack up if those are present over the whole cube at a similar position once the RM-Synthesis technique is applied in later stages of the analysis. This is also possible vice versa where strong artefacts in an individual image can be averaged out in this process and lead to a good image quality after RM-Synthesis processing.
# Stokes V represents the circular polarisation. Astronomically circularly polarised sources are extremely rare and most often show percentage polarisation of below 1%, so that Stokes V images should normally be regarded as empty.

In the following we describe the sets of metrics and the determined values for the quality assurance of the polarisation cubes/images. All values and the validation information for released beams is available in the table of the survey data release for polarisation observations.

Stokes V validation
********************
The following parameters were derived for each Stokes V  image:

* σ_in: rms in the inner part of the image, which is defined as a radius of <30′ around the central coordinate of a beam [microJy/beam]
* σ_out: rms in the outer part of the image, which is defined as a radius of >60′ around the central coordinate of a beam [microJy/beam]
* FT_max: Absolute of the Fourier Transformation of the image. This value gives a good measure of repeating structures in the image such as amplitude artefacts which manifest as stripes.
* peak_inner: The maximum of the absolute values of the inner part of the image as defined in σin (see above) [microJy/beam]
* b_min: The diameter of the FWHM minor axis of the synthesised beam [arcseconds]

A Stokes V image fails validation if one of the following criteria is met:

# σ_in and/or σ_out > 60 microJy/beam. This is the same value as for the continuum validation.
# b_min > 15''. This criterium filters any images for observations where failing or missing dishes are raising the FWHM of the synthesised beam above a value which is not acceptable for the survey.
# FT_max > 25. This value was empirically determined and filters any image, which is suffering from leftover RFI or strong amplitude errors.
# peak_inner > 4mJy. Images with values above this limit are most likely strongly affected by instrumental leakage and in most cases also show strong artefacts.

The first two criteria match that of the continuum validation and are based on survey specification. The second two criteria were empirically determined to filter images with strong polarization artefacts.
Stokes Q&U validation

Stokes Q/U cubes are validated depending on how many planes in a cube fail the following two criteria:

# The synthesised beam's minor axis of an image is larger than 17.5''. We are using a slightly larger value here compared to the continuum or Stokes V validation due to the fact that the beam becomes larger for images at lower frequencies.
# The rms noise in an image is larger than 300 microJy/beam. This corresponds to the same noise level as for the continuum and Stokes V images assuming a homogeneous noise distribution along the frequency axis. Stacking 24 images would reduce the noise by a factor of ~5.

Beams where more than one third of the images (>8) in Stokes Q or U are failing either of the above mentioned criterium do not pass the validation.

The table of released polarisation beams includes the following columns that describe the Stokes Q/U data quality:

* Qbeam_frac: Fraction of Q image planes failing criterium 1. [0.0-1.0]

* Ubeam_frac: Fraction of U image planes failing criterium 1. [0.0-1.0]

* Qnoise_frac: Fraction of Q image planes failing criterium 2. [0.0-1.0]

* Unoise_frac: Fraction of U image planes failing criterium 2. [0.0-1.0]

HI
####
Cube Validation
***************
The quality of the HI line data was validated in multiple steps. We concentrate the analysis on cubes 0, 1, and 2 (see Table 2 in the "Available data products" document for the frequency ranges of the cubes), as the quality of cube 3 always followed that of cube 2 due to both of them being in adjacent low-RFI frequency ranges.

As a first step all cubes 0, 1, and 2 where the average rms noise was larger than 3 mJy/beam were rejected. Inspection of the cubes showed that such large noise values always indicates the presence of major artefacts in the cube.

We then constructed noise histograms for cubes 0, 1 and 2 of each observation and beam combination. We made no attempt to flag any sources prior to determining the noise histogram. The HI cubes are mostly empty (i.e. consist of noise pixels) and real sources have no discernible effect on the histogram. The only exception is that all cubes 0 were blanked below 1310 MHz to remove the impact of residual RFI at these frequencies.

We also extracted representative channels as well as position-velocity slices from each cube. The cubes of 14 observations (~550 cubes) were inspected by eye for the presence of artefacts and to gauge the impact and effect of data artefacts on the noise histograms.

Artefacts generally fell in two categories: due to imperfect continuum subtraction and due to imperfect sub-bands, which we discuss in turn.

* **Continuum subtraction artefacts**

Continuum subtraction artefacts (and with it the presence of residual grating rings) add broad wings with extreme positive and negative values to the noise histogram. Trial and error showed that these wings could be robustly detected by quantifying the fraction fex of the total number of pixels with an absolute value flux value >6.75σ where σ is the standard rms noise in the cube. While adding wings of extreme value pixels to the histogram, these artefacts in general do not affect the Gaussian shape of the central part of the histogram (i.e., at low σ values).

* **Sub-band artefacts**

The presence of sub-bands with lower quality (i.e., a higher noise) manifests itself not by wings of extreme pixels but by a systematic change in the shape of the histogram through the addition of "shoulders" to the histogram (lower kurtosis). Trial and error showed that the presence of these features were best detected by comparing the rms width of the histogram with that at the level of 0.8 percent of the maximum of the histogram. We define the parameter  p0.8 or the ratio of this 0.8 percent width and the rms.

We compared our "good", "bad" or "OK" rankings as determined by eye for the 14 observations with the corresponding fex and p0.8 values.  This is illustrated in Figure 1 where we show the distribution of all cubes 2 in the  fex-p0.8 plane with the cubes which we inspected by eye color coded to indicate their quality ranking.

"Good" cubes, i.e., those with no or very minor artefacts, were concentrated in a small part of parameter space obeying the following criteria:

* rms < 3 mJy/beam
* log(fex) < -5.30
* p0.8 < 0.25 fex + 5.875

A second criterion defines cubes of OK quality, containing some minor artefacts. This consists of cubes meeting the following conditions:

* rms < 3 mJy/beam
* -5.30 < log(fex) < -4.52
* p0.8 < 0.5 fex + 7.2

The upper limit of -4.52 of the second condition is not a hard limit and a slightly different value could also have been chosen. We found however that the values used here give a good compromise in minimizing the number of false qualifications of “OK” cubes

Cubes not obeying any of these two sets of criteria were considered “bad”.
Using these conditions we defined for all cubes 0, 1 and 2 a subset of good and OK cubes. Cube 3 in all cases follows the quality designation of cube 2.

Figure 2 shows the noise histograms and a representative channel map and position velocity slice for each of the three quality categories.

Whether a cube is part of the data release is determined by the quality criteria of the corresponding continuum image. This is described in more detail in the document “Released processed data products”. The quality of each cube and the metrics used to determine that quality are included in the VO table describing the released HI observations (see "User interfaces").
