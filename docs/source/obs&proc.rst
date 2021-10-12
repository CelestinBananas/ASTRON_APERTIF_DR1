Observations & Processing
=========================

Released Observations
########################
All raw observational data from the imaging surveys through the first year of survey observations (1 July 2019 - 30 June 2020) are released. The survey medium-deep observations during this period were focused on  the Perseus-Pisces region, with an additional medium-deep field in the HETDEX region. The wide tier of the survey focused on the HETDEX region (for overlap with the LoTSS DR1), with additional coverage in the Herschel-ATLAS North Galactic Cap, and in the fall sky between 22h-0h. In total, there are 218 observations; 65 of these observations build repeated coverage of nine medium-deep fields. There are observations of 160 unique fields; with an effective field-of-view (based on spacing between fields) of 6.44 square degrees, the released observations cover just over 1000 square degrees of sky.

:numref:`dr_year1_apercal_processing_obs` shows the sky coverage of released observations, with the full four-year survey footprint shown for reference. The color coding indicates the version of the pipeline used for processing (see "Apercal versions applicable to the release" for details), where "None" means no processing was performed (see "Notes on specific observations"). "AMES" refers to observations in the medium-deep footprint, and :numref:`dr_year1_apercal_processing_ames` shows these repeated medium-deep fields separately as individual observations of a field may be processed by different versions of the pipeline.

.. figure:: images/dr_year1_apercal_processing_obs.png
  :align: center
  :width: 400
  :alt: Relative flux error
  :name: dr_year1_apercal_processing_obs

  The sky coverage of released observations, with the full four-year survey footprint shown for reference. The color coding indicates the version of the pipeline used for processing (see "Apercal versions applicable to the release" for details).

.. figure:: images/dr_year1_apercal_processing_ames.png
  :align: center
  :width: 400
  :alt: Relative flux error
  :name: dr_year1_apercal_processing_ames

   A view of the processing for medium-deep fields with repeat visits. The observations are ordered in time-order and the color code refers to the same processing as for the figure above.

Notes on the data quality/processing  for specific observations can be found here.

A machine-readable summary table of these observations can be exported using the VO infrastructure, more details are provided in section “User Interfaces”.

Primary Beam Response
#########################

Overview of primary beam shapes for Apertif
---------------------------------------------

Knowing the primary beam shape of a radio telescope is critical for deriving accurate fluxes away from the beam center. In the case of PAFs, the primary beam response, also known as the compound beam shape, must be independently measured for each compound beam as they are not constrained to have the same shape. Generally, formed beams further from the pointing center of the PAF will have more elongated shapes.

Full characterization of the Apertif primary beam is ongoing work. In this documentation we describe the methods used to measure the compound beam shapes (drift scan measurements and Gaussian process regression); describe the first release of primary beam images and plans for near-term updates; and offer an initial characterization of these released primary beam images.

We wish to emphasize that the use of the classic WSRT primary beam correction is not appropriate for Apertif. In addition to the fact that the compound beams can have non circularly symmetric shapes (see :numref:`beams_chan` ), the sizes of the primary beams are different from the classic WSRT. The Apertif front-ends fill the focal plane more efficiently than the old MFFE frontends, leading to a smaller primary beam shape. :numref:`dif_oldwsrt` shows one set of measured compound beam shapes divided by the classic WSRT primary beam shape. In addition to the elongated shapes (and offsets) visible in outer beams, the Apertif primary beam value is generally smaller than the classic WSRT primary beam value, confirming the smaller primary beam shape for Apertif.

.. figure:: images/190912_beams_chan_7-1-1024x990.png
  :align: center
  :width: 400
  :alt: Relative flux error
  :name: beams_chan

  Beam maps for all 40 apertif beams reconstructed from drift scans. Contour levels are: 0.1, 0.2, 0.4, 0.5, 0.6, 0.8. Red contours highlight the 10% and the 50% sensitivity level. These drift scans were measured in September 2019 and channel 7 corresponds to a frequency of ~ 1.363 GHz.

.. figure:: images/190918_dif_oldwsrt-1024x905.png
  :align: center
  :width: 400
  :alt: Relative flux error
  :name: dif_oldwsrt

   Compound beam shapes derived from drift scans divided by the classic WSRT primary beam. Contours are: 0.2, 0.4, 0.6, 0.8, 1.0.

Drift scan method
------------------
Beam maps are produced from drift scans performed periodically on Cygnus A (CygA hereafter). Cyg A is chosen for the drift scans since it is one of the brightest compact radio sources in the northern sky, with a brightness of 1589 Jy (Birzan et al. 2004) an extent of approximately 5′ at 1.4 GHz, which makes it an unresolved continuum source for a single WSRT dish. During the drift scan measurement the PAF is at a fixed position on the sky and Cyg A drifts through the field of view in a straight line. The separation between the drifts is 0.1 degrees in declination. This is then repeated 31 times to cover the whole field of view of the 40 Apertif beams. Figure 1 illustrates this process.

Drift scan observations are scheduled using the aperdrift code : https://github.com/kmhess/aperdrift
