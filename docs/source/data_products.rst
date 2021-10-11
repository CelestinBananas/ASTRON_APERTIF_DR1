Data Products
===============

**********
Continuum 
**********

Image validation
################
The continuum images were individually validated for every beam. In order to do this, a set of metrics was defined which inform on different aspects of image quality. The starting point of the validation are the residual images obtained after cleaning the continuum images. The validation aims at checking to what extent these images only contain Gaussian noise. The premise being that any significant deviation from this indicates issues with the calibration and/or the reduction of the data.

The following parameters were derived for each residual image.

* σin: Noise in inner half degree of the image, determined in a robust way from the residual image using the median of the absolute values.
* σout Noise at the edge of the residual image, more than a degree from the centre  determined in a robust way from the residual image using the median of the absolute values. This value is taken as a reasonable measure of the expected noise.
* R=σin/σout: A measure of the strength of artifacts left in the centre of the residual image.
* Ex-2:  Area, in units of beam area, with values below 2 σout in the inner 0.5 degree of the residual image, in excess of what expected from a purely Gaussian distribution. For perfect noise Ex-2 = 0.
* MaxNeg: the level, in units of σout, at which the area covered by pixels with values below this level is 10 beams. The expected value is -3.2. More negative values indicate significant negative calibration residuals.

Note that we did not use the equivalents of the parameters Ex-2 and MaxNeg based on positive deviations from Gaussianity (Ex+2 and MaxPos). This is because many residual images have weak, positive residuals due to insufficient cleaning which would then dominate the validation.

Visual examination of a large set of images was undertaken to define the numerical criteria that would catch significant image artifacts, as used above. The main types of image artifacts due to errors in the selfcalibration as well as strong direction-dependent errors for which the calibration pipeline did not attempt to correct. The criteria were set so that the large majority of images which were visually assessed as good would pass while only a small fraction of images that were visually assessed as bad would be classified as good.

The final criteria used to reject images are:
* R > 1.225. This criterion catches stripes due to errors in the amplitude calibration.
* R > 1.15, MaxNeg < -4.5 and Ex-2>400. This criterion catches general image artifacts and deviations from Gaussianity in the residual image.

Two additional criteria were set based on survey specifications:
* σin or σout  > 60 microJy/beam. In this case the noise of the image does not meet the  minimum requirement to be considered survey quality and valid.
* The minor axis of the restoring beam is > 15 arcsec. This occurs when both dishes RTC and RTD are missing from an observation. In this case, the required angular resolution of the survey is not met.

