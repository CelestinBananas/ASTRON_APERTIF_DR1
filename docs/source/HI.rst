HI
###
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
