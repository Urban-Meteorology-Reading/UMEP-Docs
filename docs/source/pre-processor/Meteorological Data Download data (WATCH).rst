.. _WATCH:

Meteorological Data: Download data (WATCH)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributors：
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Andy Gabey
     - Reading
   * - Ting Sun
     - Reading
   * - Helen Ward
     - Reading
   * - Lingbo Xue
     - Reading
   * - Zhe Zhang
     - Reading
   * - Tom Kokkonen
     - Helsinki
   * - Leena Järvi
     - Helsinki
   * - Sue Grimmond
     - Reading

* Introduction：
  
	  .. note:: (11/July/2019) The WATCH download plugin is not functional due to a shutdown of a data server. The UMEP team are working on a solution.

      Basic meteorological variables are required for most applications in the UMEP processor. If observed data are not available for a particular location, the global `WATCH <http://www.eu-watch.org/>`__ forcing datasets (Weedon et al. 2011, 2014) can be used to provide this information.
      The WATCH data downloader allows climate reanalysis data to be extracted for a specific location and period of interest, and (optionally) transformed into annual files in a format suitable for models within UMEP.
        -  The `WFD <Abbreviations>` dataset is based on 40-year `ECMWF <Abbreviations>` Re-analysis data (ERA-40) and is available at half-degree resolution for 1901-2001.
        -  The `WFDEI <Abbreviations>` dataset is based on `ERA <Abbreviations>`-interim re-analysis data and is available at half-degree resolution for 1979-2012.

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Variables available
     - Comments
   * - Wind speed [m s\ :sup:`-1`]
     - 10 m instantaneous
   * - Air temperature [K]
     - 2 m instantaneous
   * - Specific humidity [kg kg\ :sup:`-1`]
     - 2 m instantaneous
   * - Pressure [Pa]
     - Instantaneous surface pressure
   * - Incoming shortwave radiation [W m\ :sup:`-2`]
     - Average over previous 3 hours in WFDEI and over next 3 hours in WFD, surface flux
   * - Incoming longwave radiation [W m\ :sup:`-2`]
     - Average over previous 3 hours in WFDEI and over next 3 hours in WFD, surface flux
   * - Rainfall rate [kg m\ :sup:`-2` s\ :sup:`-1`]
     - Average over previous 3 hours in WFDEI and over next 3 hours in WFD. CRU and GPCC bias correction options.
   * - Snowfall rate [kg m\ :sup:`-2` s\ :sup:`-1`]
     - Average over previous 3 hours in WFDEI and over next 3 hours in WFD. CRU and GPCC bias correction options.


The current downscaling procedure **only** deals with WFDEI data; a module for WFD is under development.
All precipitation corrections are currently conducted based on **CRU** option.
Data is drawn from a subset of the full WATCH dataset that does not cover the entire globe but includes Europe and the majority of Asian countries excluding Russia at this time. More regions may be added in the future. The map below shows current coverage:
      
      .. figure::  /images/525px-Watch_masked.png
         :align: center

         Available data in WATCH downloader (overlaid on countries)

.. note:: Message about missing Python libraries. Follow the instruction at `link <Python_Libraries>`.

* Obtaining WATCH data via UMEP：
      .. figure::  /images/Watch_downloader_2.png
         :align: center

         Integrated WATCH data downloader: control panel

* Running the tool：
      The downloader is separated into two sections:
      
          **Download climate data**: 
          Retrieves WATCH data for all variables for the location and period of interest. This saves a NetCDF (.nc) file that contains all variables at 3 h resolution that can be used directly by ExtremeFinder.
              -  *Latitude* and *longitude*: WGS84 co-ordinates of the study location. Data is extracted from the WATCH grid cell that contains these co-ordinates.
              -  *Start time* and *End Time*: The time range of data to be downloaded (inclusive; to the nearest month)
          **Refine downloaded data**: 
          Before the WATCH data can be loaded into models such as SUEWS, it must be downscaled, separated into annual files and refined. These controls perform the refinement on the .nc file downloaded in part (1) and save the results as a text file that can be loaded into further models. The resulting file contains data at 1 hour intervals, with estimates or placeholders for meteorological variables not present in WATCH.
               -  *Site height*: Height above sea level of the desired measurement site. This applies adjustments to meteorological parameters based on the height above ground level. Data are available from 1 January 1979 to 31 December 2015.
               -  *UTC offset*: Adjusts the UTC time used in the original WATCH dataset to a local time (e.g., for Beijing time, UTC Offset = 8 h should be specified). **NOTE:** As of now the tool does not support half hour-timezones.
               -  *Rain hours per 3h*: Rain events in the location of interest may be very short – information that is lost because the WATCH data is produced at 3 h intervals, within which it is assumed rain is continuous. This control limits the duration of rain in the 1-hour file to 1, 2 or 3 hours within each 3 hour interval.
               -  *Path to LQF results*: Incorporates results data from the LQF model into the disaggregated data. Note that this feature produces one file per LQF grid cell and year.

* Considerations：
      -  **Spatial resolution**: The WATCH data are provided for half-degree grid boxes. In regions with substantial heterogeneity within these grid boxes data at the grid-box scale may be not be representative of your study site (e.g. mountainous regions, urban areas).
      -  **Temporal resolution**: The data are downloaded at 3 h resolution and are linearly downscaled to 1 h time steps during the refinement step, during which radiation data are corrected for sunrise/sunset.

* References：
      -  Kokkonen et al. (2017, in review)
      -  Ward et al. (2017, in review)
      -  Weedon GP, Gomes S, Viterbo P, Shuttleworth WJ, Blyth E, Österle H, Adam JC, Bellouin N, Boucher O and Best MJ (2011) Creation of the WATCH Forcing Data and Its Use to Assess Global and Regional Reference Crop Evaporation over Land during the Twentieth Century. `Journal of Hydrometeorology 12, 823-848 <http://journals.ametsoc.org/doi/abs/10.1175/2011JHM1369.1>`__
      -  Weedon GP, Balsamo G, Bellouin N, Gomes S, Best MJ and Viterbo P (2014) The WFDEI meteorological forcing data set: WATCH Forcing Data methodology applied to ERA-Interim reanalysis data. `Water Resour. Res. 50, 7505-7514       <http://onlinelibrary.wiley.com/doi/10.1002/2014WR015638/abstract>`__|
      -  Tan YS (2015) MSc Thesis, University of Reading
      -  Xue L (2016) MSc Thesis, University of Reading
