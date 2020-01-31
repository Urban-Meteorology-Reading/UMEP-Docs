.. _ERA5:

Meteorological Data: Download data (ERA5)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

	  .. note:: (February/2020) This plugin replaces the WATCH download plugin. To make use of this plugin you need to make additional configurations outside QGIS/UMEP (see below).
	  



* Contributors：
      .. list-table::
         :widths: 50 50
         :header-rows: 1

         * - Name
           - Institution

         * - Ting Sun
           - Reading
         * - Fredrik Lindberg
           - Gothenburg



* Introduction：
       Basic meteorological variables are required for most applications in the UMEP processor. If observed data are not available for a particular location, hourly data can be retrieved from the global `the Coopernicus programme <https://climate.copernicus.eu/>`__ and thier Climate Data Store. This plugin allows climate reanalysis data to be extracted for a specific location and period of interest (1979-2020), and transformed into formatted forcing files suitable for models within UMEP.

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
     - Average over previous 1 hour
   * - Incoming longwave radiation [W m\ :sup:`-2`]
     - Average over previous 1 hour
   * - Rainfall rate [kg m\ :sup:`-2` s\ :sup:`-1`]
     - Average over previous 1 hour


* Configuring your computer to enable download：
      - You might need to install/update the SuPy library. Follow the instruction at `link <Python_Libraries>` (**pip install supy --upgrade**).
	  - If your computer is not configured for downloading data from the Climate Data Store, follow the instructions `here <https://cds.climate.copernicus.eu/api-how-to>`__. You only need to consider the section **Install the CDS API key**.
      

* Obtaining ERA5 data via UMEP：
      .. figure::  /images/CopernicusDownloader.jpg
         :align: center

         Integrated ERA5 data downloader: control panel

* Running the tool：
      The downloader is separated into two sections:
      
          **Download climate data**: 
          Retrieves ERA5 data for all variables for the location and period of interest. 
              -  *Latitude* and *longitude*: WGS84 co-ordinates of the study location. Data is extracted from the ERA5 grid cell that contains these co-ordinates.
              -  *Start time* and *End Time*: The time range of data to be downloaded
          
* Considerations：
      -  **Spatial resolution**: The ERA5 data are provided for half-degree grid boxes. In regions with substantial heterogeneity within these grid boxes data at the grid-box scale may be not be representative of your study site (e.g. mountainous regions, urban areas).


