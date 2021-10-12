Known issues/Caveats to the user
=====================================

System notes
################
The Apertif system has not been static since the start of science operations. Small but significant changes to the system to increase stability and data quality have occurred.

One of the biggest impacts on the final quality of images is the presence of direction dependent errors, which can be attributed to antenna elements within the PAF for specific telescopes which are malfunctioning or missing from the signal chain. Another cause of direction dependent errors is due to pointing offsets of one or more telescopes.
Generally, the emphasis of system changes has been on improving the quality of the formed compound beams and pointing stability.

The most significant upgrades to the system are listed below in chronological order:

* **Synch-optics boards on RTC and RTD:**

  On 3 September 2019 and 5 August 2019, synch-optics boards were installed on dishes RTC and RTD. These two dishes are furthest from the control building. They were suffering from delay issues; due to jumps in interpreting the clock signal, the residual delays for these dishes would change by up to hundreds of nanoseconds, happening at random times during observations. The synch-optics boards stabilized the clock signal, preventing the very large residual delay that would lead to the loss of usable data from the dishes.

* **Targeted maintenance of individual elements:**

  The Apertif PAF is relatively sparsely filled. Thus, any given compound beam relies predominantly on 1-2 elements. If those elements are missing from the signal chain, that compound beam will have a non-ideal shape. When in a compound beam of on one dish, the signal of a key element is missing, this presents an odd response compared to that compound beam on all other dishes. The resulting images for that beam have strong direction dependent errors. Since October 2019, the performance and gains of individual elements are closely monitored so that they can be repaired in the most expedient manner possible.

* **Attenuation tuning of individual elements:**

  After a major maintenance, the single antenna elements need to be tuned to the nominal receiving power. If elements lie outside the accepted range of parameters, they are ignored during the calculation of the beamweights. The attenuation tuning algorithm was significantly improved starting 1 October 2019.

* **Improved beam weights calculation:**

  The beam weight measurements used to calibrate the PAF are single-dish measurements and hence heavily affected by RFI. An improved method for identifying subbands affected by RFI was implemented on 10 December 2019. This allows beam weight values that are affected by RFI to be interpolated from nearby subbands that are RFI-free, resulting in higher quality beamweights (especially at lower frequencies) which leads to an improved sensitivity of the system.

* **Updated pointing model:**

  On 11 December 2019 and on 11 June 2020, the pointing model for the dishes was updated. This corrects for pointing offsets caused by changes in the mechanical structure and physical pointing of the dishes.

**Other general caveats:**

* **Ghosts:**

  Channels 16 and 48 of each subband have a “ghost”; bad signal in these channels cause a false source to appear at the center of images. Thus, any source identified at the exact center of a pointing should be treated with extreme caution.

* **Aliasing:**

  The coarse channelization of the data into subbands uses a filter that does not have a perfectly sharp frequency response. This results in some overlap of response between adjacent subbands.  This effect is strongest for channels near a subband edge and also results in a sharp drop in overall response for channels at the subband edges, namely channels 0, 1 and 63 of every subband.  Currently, no correction is done for the aliasing. A brute force approach is used to deal with the suppressed signal at the edges of the subbands -- the low signal channels are flagged.  An offline anti-aliasing filter is under development; when it is available, aliased signals will be removed, and the sharp drop in subband response will be evened out. Until then, we note that aliased signal may occur in the presence of strong HI emission and that 3/64 channels are flagged at full spectral resolution. The impact of this flagging on the spectrally-averaged line cubes is described in the "External Comparison" section of the HI validation.



* **Telescope specific issues:**

  Due to operational needs (exceptional maintenance) or because of failures (the above mentioned high residual delay issue, tracking issues, extreme RFIs, etc), one or more telescopes could be missing from an observation. Information about specific observations can be found in "Notes on specific observations".

Notes on specific observations
#################################
This section provides brief notes on observations that had observational or processing issues. This list is not exhaustive, and the user is always encouraged to examine the data and inspection plots closely.

Observations with no released processed data
************************************************

Some observations have no released processed data associated with them. This can either be because they were processed with the 300 MHz version of the pipeline, which produced lower quality data products, or because the automatic identification of calibrators by AUTOCAL (see "Apercal overview") and subsequent processing failed. In addition, there is a set of observations that were scheduled without RTC & RTD, thus failing to be validated for release since they did not meet the minimum resolution requirement.

Early processing
---------------------
The following observations have no released processed data products because they were processed with the 300 MHz version of the pipeline, which did not produce data products of the required quality.

.. csv-table:: Observations processed with 300 MHz version of pipeline.
  :align: center
  :header: "ObsID", 	"Field"
  :widths: 20, 20
  :name: early_proc

  190711169,  	S2152+4114
  190712041,  	M1403+5324
  190713001,  	M0155+3130
  190713042,  	S2323+2904
  190714041, 	S1444+5058
  190718124,  	S2146+4340
  190719041, 	S1242+5058
  190719042,  	M0155+3130
  190720041,  	S2336+2904
  190721041, 	S1426+5058
  190722001, 	M0208+3130
  190725041,  	S1236+6041
  190725042,  	M0155+3130
  190726041,  	S2319+3130
  190727041,  	S1439+5324
  190727042,  	M0208+3356

Autocal failures
---------------------
The following observations have no ingested processed data products because the automatic running of the pipeline failed in their case. Generally this was because of an issue with identifying calibrators. These observations can be manually reprocessed. Access to the raw data can be requested via the helpdesk.


.. csv-table::  Observations not processed due to failure of automatic calibration identification. Notes: *Observations 028-033 failed. **Go backwards for a pol cal that has C/D (see Obs fails below).
  :align: center
  :header: "ObsID", 	Field", 	"FluxCal: ObsIDs", 	"Polcal: ObsIDs"
  :widths: 20, 20, 20, 20
  :name: autocal_fail

  190728041, 	S2258+2904, 	3C147: 190727 001-040, 	3C286: 190728 001-040
  190731125, 	S2227+3130, 	"3C147: 190801  001-040\*", 	3C286: 190731 085-124
  190806345, 	S2311+2904, 	3C147: 190807 001 - 040, 	3C286: 190808 001-040
  200429042, 	S1446+3848, 	3C147: 200429 002 - 041, 	"3C138: 200428 001 - 040\*\*"


Observational failures
-------------------------
If RTC and RTD are unavailable, an observation is considered failed. Some of the early observations from July, which don’t have processed data available, may suffer from this as both RTC and RTD had issues with delay jumps (see System notes). In addition, there are a series of observations from April/May which were inadvertently scheduled without RTC and RTD and thus don’t have processed data which passes validation. These observations are:

.. csv-table:: Observations scheduled without RTC & RTD.
  :align: center
  :header: "ObsID", 	"Field"
  :widths: 20, 20
  :name: obs_fail

  200430053, 	S1131+6041
  200501001,   	S2346+5324
  200501042, 	S2346+5324
  200502054,   	S1142+5550
  200503001,  	S2358+4832
  200503042,  	S1443+3622
  200505016, 	S0001+4606
  200505057, 	S1446+3848


Partially processed observations
************************************
Calibrator identification issues
-------------------------------------
  Two observations, 191207034 and 191207035, do not have processed data products for the first seven beams, as those beams (due to scheduling complications) were not properly identified by AUTOCAL. Given the small number of beams missing, they were not reprocessed. These observations can be manually reprocessed. Access to the raw data can be requested via the helpdesk.


Reprocessed observations
**************************
Reprocessed with manual flags
------------------------------
As part of the data release, observations where essentially all beams failed validation (e.g., four or fewer beams passed) were visually inspected to identify the cause. In some cases there were no obvious causes, other than bright sources in the field. In other cases, inspection revealed an antenna was off-source (e.g., stuck) during the observation or part of the observation occurred while the target field was not visible. In order to increase the quality of the processed data from these fields, they were manually reprocessed with the additional, visually identified, flags applied. Other fields may also benefit from individual flags and reprocessing.

These observations are:

.. csv-table:: Observations manually reprocessed with additional flags.
  :align: center
  :header: "ObsID", 	"Field", "Note"
  :widths: 20, 20, 20
  :name: reprocessed

  191024043, 	S1402+3622, 	"Flag RT2, plus first five minutes"
  191024044, 	M0155+3622, 	Flag RT2
  191209025, 	M1342+2904, 	Flag RT9
  191227014, 	M0155+3356, 	"Flag RT9, plus ~15 minutes of RTA due to extra shadowing (by  stuck RT9)""
  191230041, 	S2300+3848, 	Flag RT9
  191031242, 	M0155+3622, 	Flag first ten minutes
  200305001, 	M0141+3622, 	Flag last 1h10min
  200427042, 	S1427+3130, 	Flag RTB


Reprocessed with correct polarization calibrator
-------------------------------------------------
There were two observations where AUTOCAL incorrectly assigned the same flux calibrator to be both the flux and polarization calibrator to the initial call of Apercal. These observations were reprocessed with the correct polarization calibrator.

.. csv-table:: Observations manually reprocessed with correct polarization calibrator.
  :align: center
  :header: "ObsID", 	Field", 	"FluxCal: ObsIDs", 	"Polcal: ObsIDs"
  :widths: 20, 20, 20, 20
  :name: man_reproc

  200126082, 	S1428+5815, 	3C147: 200126 042 - 081, 	3C286: 200126 001  - 040
  200406054, 	S1611+5324, 	3C147: 200406 014 - 053, 	3C286: 200405002 - 612

Data quality notes
***********************
Problems with polarization data
---------------------------------
There is one dataset which has no polarized data products as a polarized calibrator was not able to be observed in the same observational setup. This is ObsID 200309042, field S1042+5324.

In addition, the observation 200505057 was processed without a polarization calibrator. However, since it has no released processed data due to missing RTC and RTD and thus failing resolution requirements, it was not reprocessed. These observations can be manually reprocessed. Access to the raw data can be requested via the helpdesk.
