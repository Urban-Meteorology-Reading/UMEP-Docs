.. _Processor:


Processor
---------

Outdoor Thermal Comfort: SOLWEIG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Fredrik Lindberg

* Introduction:
    -  The **SOLWEIG** plugin can be used to calculate spatial variations of mean radiant temperature (T~mrt~) and radiant fluxes using digital surface models (DSM) and ground cover information. Optionally, vegetation DSMs could also be used. The methodology that is used to generate shadows originates from Ratti and Richens (1990) and is further developed and described in Lindberg and Grimmond (2011) and Lindberg et al. (2016). The current version of the model is 2016a.
    -  The full manual of the SOLWEIG model can be found `here <http://urban-climate.net/umep/SOLWEIG>`__.

* Location:
  - The SOLWEIG model is located at
      -  UMEP
        -  Processor
          -  Outdoor Thermal Comfort
            -  SOLWEIG

* Related Preprocessors：
  - `MetdataPreprocessor <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_MetPreprocessor>`__, `Download data (WATCH) <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_Download_data_.28WATCH.29>`__, `SkyViewFactor Calculator <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Geometry:_Sky_View_Factor_Calculator>`__, `Wall Height and Aspect <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Geometry:_Wall_Height_and_Aspect>`__, `LandCoverReclassifier <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Reclassifier>`__   |

* Dialog box：
      .. figure:: /images/SOLWEIG.png

* Dialog sections ：
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Spatial data
     - Spatial input data is specified
   * - Meteorological data
     - Meteorological input data is specified, as a continuous file or specific momentary values.
   * - Environmental parameters
     - Possibilities to alter emissiveties and albedos for the different urban surfaces.
   * - Optional settings
     - Here additional setting such as including POIs (Points of Interest) is found.
   * - Human exposure parameters
     - Settings for calculating mean radiant temperature.
   * - Output maps
     - Options to choose the geotiffs to be saved for each iteration.


.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Building and Ground DSM
     - A DSM consisting of ground and building heights. This dataset also decides the latitude and longitude used for the calculation of Sun position.
   * - Vegetation Canopy DSM
     - A DSM consisting of pixels with vegetation heights above ground. Pixels where no vegetation is present should be set to zero.
   * - Vegetation Trunk Zone DSM
     - A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground. Pixels where no vegetation is present should be set to zero.
   * - Use vegetation scheme
     - Tick this box if you want to include vegetation (trees and bushes) in the calculations.
   * - Trunk Zone DSM Exist
     - Tick this in if a trunk zone DSM already exist.
   * - Transmissivity of Light Through Vegetation (%)
     - Percentage of light that is penetrating through vegetation. Default value is set to 3 % according to Konarska et al. (2013).
   * - Percent of Canopy Height
     - If a trunk zone vegetation DSM is absent, this can be generated based on the height of the Canopy DSM. The default percentage is set to 25%.
   * - Save generated Trunk zone DSM
     - Tick this in if you want to save your TDSM that is generated.
   * - Use land cover scheme
     - Available since v2015a. Land cover grid should be in the UMEP standard format **except** for the two tree classes (deciduous and conifer) as the land cover grid should represent what is on the ground surface. UMEP land cover grid can be prepared in the Pre-processor.
   * - Use land cover grid to produce building grid
     - Tick this in if the building grid should be created from the land cover grid. Otherwise, a DEM including only ground heights must be added. This will then be used to derive a building grid together with the ground and building DSM.
   * - Save generated building grid
     - Tick this in if you want to save the boolean building grid that is generated.
   * - SkyViewFactor grids
     - The SOLWEIG model make use of SVFs to calculate T\ :sub:`mrt`. The zip-file needed can be created with the SkyViewFactor calculator found in the UMEP Pre-processor.
   * - Wall height raster
     - The SOLWEIG model make use of wall height raster to calculate T\ :sub:`mrt`. This can be calculated using the Wall height and aspect plugin found in the UMEP Pre-processor
   * - Wall aspect raster
     - The SOLWEIG model make use of wall height raster to calculate T\ :sub:`mrt`. This can be calculated using the Wall height and aspect plugin found in the UMEP Pre-processor.

*  Meteorological data：
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Use continuous meteorological dataset
     - Tick this in if a time series of data should be used. The specific format could be prepared in the UMEP Pre-processor.
   * - Estimate diffuse and direct components from global radiation
     - Tick this box if diffuse and direct shortwave radiation is unavailable. The Reindl et al. (1990) model is used to calculate diffuse radiation. Direct radiation perpendicular to the solar beam should be considered.
   * - Settings for one iteration.
     - If a meteorological dataset is not used there is a possibility to run the model for one iteration using the calendar and spin-boxes to set meteorological variables present here. The default values are for a clear Summer day at 1230 in Göteborg, Sweden.
   * - UTC offset
     - Time zone needs to be specified. Positive numbers moving east (e.g. Stockholm UTC +1).


*  Optional settings：

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Include POIs
     - By ticking in the option to include POIs (Point of Interest), a vector point layer can be added and full model output are written out to text files for the specific POI. Multiple POIs can be used by including many points in the vector file. See the `full manual <http://www.urban-climate.net/umep/SOLWEIG>`__ for more information.
   * - Adjust sky-emissivity according to Jonsson et al. (2006)
     - Tick this box to include adjustment (0.04) of sky emissivity which was present in the earlier versions of the SOLWEIG model (not recommended).
   * - Consider human as cylinder instead of box
     - Tick this box to consider man as a cylinder instead of a box according to Holmer at al. (2015).

* Environmental parameters：
      - Emissivity (ground)||Emissivity of ground. Not used if land cover scheme is activated.
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Albedo (buildings)
     - Albedo of building walls and roofs.
   * - Albedo (ground)
     - Albedo of ground surfaces. Not used if land cover scheme is active.
   * - Emissivity (walls)
     - Emissivity of building walls and roofs.
   * - Emissivity (ground)
     - Emissivity of ground. Not used if land cover scheme is activated.

* Human exposure parameters ：
      -  Posture of the human body||Choose between standing (default) and sitting.

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Absorption of shortwave radiation
     - Amount of shortwave radiation that the human body absorb.
   * - Absorption of longwave radiation
     - Amount of longwave radiation that the human body absorb.
   * - Posture of the human body
     - Choose between standing (default) and sitting.


* Output maps:
     - A number of different outputs can be chosen here. All grids will be written out as GeoTIFFs at the location specified as the output folder.

* Run:
     - Starts the calculations. As SOLWEIG is a 2.5D model, large grids (i.e. high number of pixels) will take a relatively long time to compute. The model is embedded in a so called worker which means that you can continue working with QGIS while the model runs.

* Add Average mean radiant temperature to the map canvas:
     -  If ticked, an average T\ :sub:`mrt` map will be added to the current

* Close:
     - Closes the plugin.

* Quick example on how to run SOLWEIG：
       presented:
             #. Download and extract (unzip) the test dataset (`testdata\_UMEP.zip <https://bitbucket.org/fredrik_ucg/umep/downloads/testdata_UMEP.zip>`__).
             #. Add the raster layers (DSM, CDSM and land cover) from the Goteborg folder into a new QGIS session. The coordinate system of the grids is **Sweref99 1200 (EPSG:3007)**.
             #. In order to run SOLWEIG, some additional datasets must be created based on the raster grids you just added. Open the SkyViewFactor Calculator from the UMEP Pre-processor and calculate SVFs using both your DSM and CDSM. Leave all other settings as default.
             #. Open the Wall height and aspect plugin from the UMEP Pre-processor and calculate both wall height and aspect using the DSM and your input raster. Tick in the box to add them to your project. Leave all other settings as default.
             #. Now you are ready to generate your first T\ :sub:`mrt` map. Open SOLWEIG and use the settings as shown in the figure below but replace the paths to the fit your computer environment. When you are finished, press *Run*.

                .. figure:: /images/SOLWEIGfirsttry.png
                There is also a meteorological file present in the test dataset that can be used to run the model for a whole day.

* Remarks ：
      -  All DSMs need to have the same extent and pixel size.
      -  This plugin is computationally intensive i.e. large grids will take a lot of time and very large grids will not be possible to use. Large grids e.g. larger than 4000000 pixels should preferably be tiled before.
      -  SOLWEIG focus on pedestrian radiation fluxes and it is not recommended to consider fluxes on building roofs.

* References：
      -  Holmer, B., Lindberg, F., Rayner, D. and Thorsson, S. 2015: How to transform the standing man from a box to a cylinder – a modified methodology to calculate mean radiant temperature in field studies and models, ICUC9 – 9 th International Conference on Urban Climate jointly with 12th Symposium on the Urban Environment, BPH5: Human perception and new indicators. Toulouse, July 2015.
      -  Konarska J, Lindberg F, Larsson A, Thorsson S, Holmer B 2013. Transmissivity of solar radiation through crowns of single urban trees—application for outdoor thermal comfort modelling. `Theoret. Appl. Climatol., 1–14 <http://link.springer.com/article/10.1007/s00704-013-1000-3>`__
      -  Lindberg, F., Grimmond, C.S.B., 2011a. The influence of vegetation and building morphology on shadow patterns and mean radiant temperatures in urban areas: model development and evaluation. `Theoret. Appl. Climatol. 105, 311–323 <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
      -  Riendl D.T., Beckman W.A. and Duffie J.A. (1990), Diffuse Fraction Correlations, Solar Energy, Vol. 45, No.1, pp. 1-7.



Outdoor Thermal Comfort: ExtremeFinder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Bei Huang (Reading), Andy Gabey (Reading)

* Current Options:
     -  Identifies extreme high events (e.g. Heat waves) and low events (e.g. Cold Waves). Designed primarily for temperature data (heat waves identified from daily maximum and mean T; cold waves from daily minimum), but can also be used to indicate potential high and low extremes in other meteorological variables.

* Data must be provided by the user, and can be:
     -  Previously-downloaded WATCH data in a NetCDF (.nc) file (this can be obtained from the WATCH downloader)
     -  Other NetCDF (.nc) file containing sub-daily measurements, or daily maximum/mean/minimum values. Must contain a **'time**' dimension, and variable(s) with name(s) matching those being analysed using the ExtremeFinder.
     -  Text (.txt) file, daily T\ :sub:`max`, T\ :sub:`avg` or T\ :sub:`min` (`file sample <http://www.urban-climate.net/watch_data/data%20set%20sample.txt>`__: 1979-01-01 to 2009-12-31). Only temperature analysis can be performed using a text file.

* Method ：
      —  Basis for thresholds - set into Input.nml (namelist)
            -  `Meehl and Tebaldi (2004) <http://science.sciencemag.org/content/305/5686/994>`__: 81st, 97.5th
            -  `Fischer and Schär (2010) <http://www.nature.com/ngeo/journal/v3/n6/full/ngeo866.html>`__: 90th
            -  `Vautard et al. (2013) <https://link.springer.com/article/10.1007%2Fs00382-013-1714-z>`__: 90th
            -  `Schoetter et al. (2014) <https://link.springer.com/article/10.1007/s00382-014-2434-8>`__: 98th
            -  `Sirje Keevallik (2015) <http://www.kirj.ee/26593/?tpl=1061&c_tpl=1064>`__: 10th
            -  `A. K. Srivastava (2009) <http://onlinelibrary.wiley.com/doi/10.1002/asl.232/abstract>`__: 3 °C
            -  Busuioc et al. (2010): 5 °C

* Location:
  -  UMEP
    -  Processor
      -  Outdoor Themal Comfort
        -  ExtremeFinder

* Dialog box:
       .. figure:: /images/Extremefinder3.png
       The interface for the ExtremeFinder plugin

* Steps to use:
      #. Select climate data: The ExtremeFinder will use all the data available in its analysis. You will be prompted for a text (.txt) or NetCDF (.nc) file:

         -  *NetCDF file*: The latitude, longitude, start and end date boxes will be populated automatically, if the data is available in the NetCDF file.
         -  *Text file*: The latitude, longitude, start and end date boxes must be filled in by the user, as the information is needed in calculations:

            -  *Latitude* (degrees N) and *Longitude* (degrees E) are WGS84 co-ordinates
            -  *Start* and *end date* are inclusive and must match the data extent

      #. Select the *extreme event type* and the *calculation method*:

         -  Event types are either Extreme *high* (e.g. Heat wave) or *low* (e.g. Cold wave)
         -  There are several different ways to identify extremes, depending on the event type
         -  Choose the *meteorological variable* to analyse for extremes

            -  **Note:** The methods in the Extreme Finder are based on Tair and may not be appropriate for other variables

      #. Select Output File: A list of extreme events will be written to the file

         -  Note: this will be overwritten if not a new name

      #. Run: Performs the analysis

# Output: Extreme events (heat waves used as example below) ：
      #. Daily T\ :sub:`max` (or T\ :sub:`avg` / T\ :sub:`min`) with time (Y= Year, X=Month)

         -  Colour gives Temperature (see key)
         -  Yellow Box Highlights Heatwave (Coldwave) periods This loads the model interface dialog box:
              .. figure:: /images/350px-TMax1.jpg
              Heat/Cold wave periods

      #. Box plot of distribution of heat (cold) wave by year.

         -  whiskers =1.5\* IQR
         -  outliers
            - any data beyond the whiskers
              .. figure:: /images/350px-HW_Box.jpg
              Box-and-whisker plot of Heat/Cold wave days each year

      #. Number of heat (cold) waves days per year
            .. figure:: /images/350px-HWDays.jpg
            Histogram showing number of Heat/Cold wave days each year


Urban Energy Balance: GQ\ :sub:`F`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Andy Gabey (Reading), Izzy Capel Timms (Reading), Sue Grimmond (Reading)
* How to Cite:
     -  Gabey A, S Grimmond, I Capel-Timms 2018: Anthropogenic Heat Flux: advisable spatial resolutions when input data are scarce Theoretical and Applied Climatology https://doi.org/10.1007/s00704-018-2367-y
     -  Lindberg F, CSB Grimmond, A Gabey, B Huang, CW Kent, T Sun, NE Theeuwes, L Järvi, H Ward, I Capel-Timms, YY Chang, P Jonsson, N Krave, DW Liu, D Meyer, KFG Olofson, JG Tan, D Wästberg, L Xue, Z Zhang 2018: Urban multiscale environmental predictor (UMEP) - An integrated tool for city-based climate services Environmental Modelling and Software 99, 70–87 10.1016/j.envsoft.2017.09.020

* Introduction:
      `See separate manual <http://urban-climate.net/umep/GQF_Manual>`__
* Location:
    - The GreaterQF plugin is located at
        -  UMEP
          -  Processor
            -  Urban Energy Balance
              -  GreaterQF
* Dialog box：
        .. figure:: /images/GQF.png

* Dialog sections：
        - The model run is configured using the dialog box:
              -  *Start date* and *end date*: The first and final dates for which the model should be run.
              -  *Output areas*: Two options are currently available: Local authority areas and 1km grid. These select the spatial units of the model calculations.
              -  *Include QF components*: The components of anthropogenic heat flux for the model to include in calculations.
              -  *Output path*: A directory that houses model outputs.

* Model outputs ；
      - **Example map**
          - The total anthropogenic heat flux for the first time step is displayed in QGIS to demonstrate model output and the output areas. In order for these areas to be displayed correctly, the coordinate reference system must be selected. The QGIS “Select CRS” screen will appear, and EPSG 27700 (British National Grid) must be chosen.
          - The layer displaying model output also contains the other contributions to QF (e.g. car transport). These can be visualised using standard QGIS methods of styling the layer according to the selected component, or inspecting the layer attributes table.
      - **CSV files**
          -  A CSV file is generated for each of the 19 contributions to QF (e.g. car travel, wastewater heating) and the total QF. Each file contains a column per output area (shown in the example map) and a row per time step. These are labelled accordingly. The filenames are abbreviated where necessary for compatibility, with the following convention used:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - El
     - Electricity
   * - Gas
     - Gas
   * - Dm
     - Domestic use
   * - Id
     - Industrial use
   * - Tspt
     - Transport
   * - Unre
     - Unrestricted electricity (non-Economy 7)
   * - Eco7
     - Economy 7 electricity
   * - Everything
     - Grand total QF across all sources

          -  A “pickled” Python data object containing the results is also saved in the local temporary folder for future use with other UMEP components.

*  References  ：
      -  Iamarino M, Beevers S & Grimmond CSB (2012) High-resolution (space, time) anthropogenic heat emissions: London 1970-2025 `International J. of Climatology 32, 11, 1754-1767 <http://doi.wiley.com/10.1002/joc.2390>`__
      -  Gabey A, S Grimmond, I Capel-Timms 2018: Anthropogenic Heat Flux: advisable spatial resolutions when input data are scarce Theoretical and Applied Climatology https://doi.org/10.1007/s00704-018-2367-y
      -  Lindberg F, CSB Grimmond, A Gabey, B Huang, CW Kent, T Sun, NE Theeuwes, L Järvi, H Ward, I Capel-Timms, YY Chang, P Jonsson, N Krave, DW Liu, D Meyer, KFG Olofson, JG Tan, D Wästberg, L Xue, Z Zhang 2018: Urban multiscale environmental predictor (UMEP) - An integrated tool for city-based climate services Environmental Modelling and Software 99, 70–87 10.1016/j.envsoft.2017.09.020

Urban Energy Balance: LQ\ :sub:`F`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
      Andy Gabey (Reading), Izzy Capel-Timms (Reading),
      Sue Grimmond (Reading), Sam Jackson (Reading),
      XY Ao (SIMS), Bei Huang(Tsinghua Unviersity)

* Introduction  ：
          - `See separate manual <http://urban-climate.net/umep/LQF_Manual>`__

* References  ：
          -  Allen, L., Lindberg, F. and Grimmond, C. (2011) Global to city scale urban anthropogenic heat flux: model and variability. `International Journal of Climatology 31:13, 1990-2005. <http://onlinelibrary.wiley.com/doi/10.1002/joc.2210/abstract>`__
          -  Lindberg, F., Grimmond, C., Yogeswaran, N., Kotthaus, S. and Allen, L. (2013a) Impact of city changes and weather on anthropogenic heat flux in Europe 1995–2015. `Urban Climate 4, 1-15. <http://www.sciencedirect.com/science/article/pii/S2212095513000059>`__
          -  Gabey A, S Grimmond, I Capel-Timms 2018: Anthropogenic Heat Flux: advisable spatial resolutions when input data are scarce Theoretical and Applied Climatology https://doi.org/10.1007/s00704-018-2367-y
          -  Lindberg F, CSB Grimmond, A Gabey, B Huang, CW Kent, T Sun, NE Theeuwes, L Järvi, H Ward, I Capel-Timms, YY Chang, P Jonsson, N Krave, DW Liu, D Meyer, KFG Olofson, JG Tan, D Wästberg, L Xue, Z Zhang 2018: Urban multiscale environmental predictor (UMEP) - An integrated tool for city-based climate services Environmental Modelling and Software 99, 70–87 https://10.1016/j.envsoft.2017.09.020

Urban Energy Balance: Urban Energy Balance (SUEWS, simple)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Fredrik Lindberg (Gothenburg), Sue Grimmond
 * Introduction：
        - SUEWS can be run as a standalone or via UMEP (see `SUEWS Manual <http://urban-climate.net/umep/SUEWS>`__).
        - This plugin makes it possible to run a simplified version of the Surface Urban Energy and Water Balance Scheme (SUEWS). For a full version of the model, the SUEWS/BLUEWS (Advanced) plugin can be used. It is also available as a separate program.
        - SUEWS (Järvi et al. 2011, 2014, Ward et al. 2016a, b) simulates the urban radiation, energy and water balances using commonly measured/modeled meteorological variables and information about the surface cover. It utilizes an evaporation-interception approach (Grimmond et al. 1991), similar to that used in forests, to model evaporation from urban surfaces.
        - The model uses seven surface types: paved, buildings, evergreen trees/shrubs, deciduous trees/shrubs, grass, bare soil and water. The surface state for each surface type at each time step is calculated from the running water balance of the canopy where the evaporation is calculated from the Penman-Monteith equation. The soil moisture below each surface type (excluding water) is taken into account.
        - The model distributed with this manual can be run in two standard ways:
              -  For an individual area
              -  For multiple areas that are contiguous. There is no requirement for the areas to be of any particular shape but here we refer to them as ‘grids’.
        - Model applicability: Local scale – so forcing data should be above the height of the roughness elements (trees, buildings). SUEWS Simple is designed to be executed for a single location but the model is also able to be executed on a grid.

* Location:
    - The SUEWS Simple plugin is located at
        -  UMEP
          -  Processor
            -  Urban Energy Balance
              -  Urban Energy Balance (SUEWS, Simple)

* Related Preprocessors ：
      -  `MetdataPreprocessor <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_MetPreprocessor>`__, `Download data (WATCH) <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_Download_data_.28WATCH.29>`__, `LandCoverReclassifier <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Reclassifier>`__, `LandCoverFraction (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Fraction_.28Point.29>`__, `Image Morphometric Parameters Calculator (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Image_Morphometric_Parameters_Calculator_.28Point.29>`__, `Foot Print Model (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Source_Area_.28Point.29>`__

* Dialog Box：
    .. figure:: /images/SuewsSimple.png

* Dialog sections：
      .. list-table::
         :widths: 50 50
         :header-rows: 0

         * - far right
           - provides some tips and tricks for running the model.
         * - other four
           - to specify user-defined input data, either manually or by using the appropriate UMEP-plugin in the per-processor.
         * - bottom
           - to make some additional settings as well as running the model.


* prepared dataset:
     - SUEWS Simple comes with a prepared dataset that can be used for testing. This can be utilized by pressing **Add settings from test dataset**. This dataset is a fictitious dataset from the central parts of London.

* Building Morphology:
     -  The three site specific building morphology parameters needed are usually derived from Digital Surface Models DSMs. However, they also can be entered manually.
           -  To use an already generated text file from the Image Morphometric Calculator (Point) plugin.
           -  To open the plugin from SUEWS Simple and generate the data.
     -  If an already generated text file is used, the **isotropic file** should be used (see Image Morphometric Calculator (Point)).

* Tree Morphology:
     -  Three site specific tree morphology parameters need to be specified. These can be derived from a Canopy DSMs that include vegetation heights. This can be entered manually or from the Image Morphometric Calculator (Point) plugin. When the plugin is used there are two options:
              -  To use an already generated text file from the Image Morphometric Calculator (Point) plugin.
              -  To open the plugin from SUEWS Simple and generate the data.
     -  If an already generated text file is used, the **isotropic file** should be used (see Image Morphometric Calculator (Point)).

* Land Cover Fractions ：
     -  Land cover fractions should add up to a total of 1. Values can be derived from a UMEP land cover dataset which can be generated via the Land Cover Reclassifier plugin in UMEP. The values can be entered manually or directly from the Land Cover Fraction (Point) plugin. If the plugin is used, there are two options:
               -  To use an already generated text file from the Land Cover Fraction (Point) plugin.
               -  To open the plugin from SUEWS Simple and generate the data.

* Initial Conditions:
     - The initial conditions are entered here. These relate to time of year, days since rain, soil moisture state and daily mean air temperature at the beginning of a model run. The state of the leaf cycle sets a rough estimate of leaf area index based on season. To adjust this in more detail, the SUEWS, BLUEWS (Advanced) plugin should be used.

* Meteorological File:
     -  The location and filename (.txt) of the meteorological file should be specified here. The format used in most UMEP-related plugins where meteorological data is required can be generated using the Metdata Processor in UMEP. For details, see the help section in the Metdata Processor or the SUEWS manual (Ward et al. 2016a).

* Output Folder:
     -  Specify a folder where you would like all the model results to be saved to. Make sure that you have write capabilities to the specified folder.
     -  *Note if you put it within the UMEP plugin folder– be careful that you do not lose any results if you update the plugin by deleting it first.*

* Year:
     - Specify what year you are running.

* Latitude:
     - Specify the latitude in decimal degrees. Positive numbers indicate Northern Hemisphere.

* Longitude:
     -  Specify the longitude in decimal degrees. Positive numbers are to the West.

* Population Density:
     - Specify the population density in people/ha (hectare) around the area of interest.

* Show Basic Plots of Model Results:
     -  Tick this box in if you would like to generate some simple plots of the result from a model run. This requires that the matplotlib library is added to your QGIS installation.

* Add Settings from Test Dataset:
     - This is recommended if you want to try the model for the first time. This uses a year long dataset from London, UK.

* Run:
     -  Button starts the model. All inputs must be set prior to this button being available.

* Close:
     -  Button closes the plugin.

* References:
      -  Järvi L, Grimmond CSB & Christen A (2011) The Surface Urban Energy and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver `J. Hydrol. 411, 219-237. <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
      -  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB (2014) Development of the Surface Urban Energy and Water balance Scheme (SUEWS) for cold climate cities, Geosci. Model Dev. 7, 1691-1711, `doi:10.5194/gmd-7-1691-2014 <http://www.geosci-model-dev.net/7/1691/2014/>`__.                                                                                                                                                                                                                                                                        |
      -  Ward HC, L Järvi, S Onomura, F Lindberg, CSB Grimmond (2016a) `SUEWS Manual <http://urban-climate.net/umep/SUEWS>`__: Version 2016a
      -  Ward HC. S Kotthaus, L Järvi, CSB Grimmond (2016b) Surface Urban Energy and Water Balance Scheme (SUEWS): development and evaluation at two UK sites `Urban Climate (in press) <:File:SUEWS_UKEvaluationPaper_Revised_v1-03.pdf>`__.

Urban Energy Balance: Urban Energy Balance (SUEWS/BLUEWS, advanced)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Fredrik Lindberg (Gothenburg)

* Introduction:
     - This plugin makes it possible to run the Surface Urban Energy and Water Balance Scheme (SUEWS). SUEWS is also available as a separate program and a simplified version within UMEP (SUEWS Simple).
     - SUEWS (Järvi et al. 2011, 2014, Ward et al. 2016a, b) simulates the urban radiation, energy and water balances using commonly measured/modeled meteorological variables and information about the surface cover. It utilizes an evaporation-interception approach (Grimmond et al. 1991), similar to that used in forests, to model evaporation from urban surfaces.
     - The model uses seven surface types: paved, buildings, evergreen trees/shrubs, deciduous trees/shrubs, grass, bare soil and water. The surface state for each surface type at each time step is calculated from the running water balance of the canopy where the evaporation is calculated from the Penman-Monteith equation. The soil moisture below each surface type (excluding water) is taken into account.
     - Model applicability: Local scale – so forcing data should be above the height of the roughness elements (trees, buildings)
* Location:
    - The SUEWS Simple plugin is located at
        -  UMEP
          -  Processor
            -  Urban Energy Balance
              -  Urban Energy Balance (SUEWS/BLUEWS, Advanced)

* Related Preprocessors:
      - `MetdataPreprocessor <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_MetPreprocessor>`__, `Download data (WATCH) <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_Download_data_.28WATCH.29>`__, `LandCoverReclassifier <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Reclassifier>`__, `LandCoverFraction (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Fraction_.28Point.29>`__, `LandCoverFraction (Grid) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Land_Cover:_Land_Cover_Fraction_.28Grid.29>`__, `Image Morphometric Parameters Calculator (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Image_Morphometric_Parameters_Calculator_.28Point.29>`__, `Image Morphometric Parameters Calculator (Grid) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Image_Morphometric_Parameter_Calculator_.28Grid.29>`__, `Foot Print Model (Point) <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Source_Area_.28Point.29>`__

* Dialog box ：
      .. figure:: /images/SuewsAdvanced.png

* Dialog sections:
     -  When you run the plugin, you will see the dialog shown below. To use this plugin, all input data needs to be prepared beforehand. This can be done using the various plugins in the pre-processor in UMEP. The settings available in this plugin is used for specifying the settings for a specific model run. You should consult the manual (`1 <http://www.urban-climate.net/umep/SUEWS>`__) for instructions and information on what settings to use. For extensive models run it is recommended to execute the model outside of QGIS (see manual). The interface below creates a so-called namelist (**RunControl.nml**) that is used be the model for general settings. After running the model, this file can be found in the suewsmodel directory in the UMEP plugin directory.

* References:
      -  Järvi L, Grimmond CSB & Christen A (2011) The Surface Urban Energy and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver `J. Hydrol. 411, 219-237. <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
      -  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB (2014) Development of the Surface Urban Energy and Water balance Scheme (SUEWS) for cold climate cities, Geosci. Model Dev. 7, 1691-1711, `doi:10.5194/gmd-7-1691-2014 <http://www.geosci-model-dev.net/7/1691/2014/>`__.                                                                                                                                                                                                                                                                        |
      -  Ward HC, L Järvi, S Onomura, F Lindberg, CSB Grimmond (2016a) `SUEWS Manual <http://urban-climate.net/umep/SUEWS>`__: Version 2016a
      -  Ward HC. S Kotthaus, L Järvi, CSB Grimmond (2016b) Surface Urban Energy and Water Balance Scheme (SUEWS): development and evaluation at two UK sites `Urban Climate (in press) <:File:SUEWS_UKEvaluationPaper_Revised_v1-03.pdf>`__.



Solar Radiation: Daily Shadow Pattern
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Fredrik Lindberg (Gothenburg)

* Introduction:
     -  The **Shadow generator** plugin can be used to generate pixel wise shadow analysis using ground and building digital surface models (DSM). Optionally, vegetation DSMs could also be used. The methodology that is used to generate shadows originates from Ratti and Richens (1990) and is further developed and described in Lindberg and Grimmond (2011). Position of the Sun is calculated using **PySolar**, a python library for various Sun related applications ([2](http://pysolar.org/)).

* Location:
    - The Shadow Generator is located at
        -  UMEP
          -  Processor
            -  Solar Radiation
              -  Daily Shadow Pattern

* Dialog box ：
      .. figure:: /images/Shadow_generator.jpg

* Dialog sections：
      .. list-table::
         :widths: 50 50
         :header-rows: 0

         * - top
           - input data is specified
         * - middle
           - setting for positioning the Sun on the hemisphere
         * - bottom
           - to specify the output and to run the calculations

* Building and Ground DSM:
     - A DSM consisting of ground and building heights. This dataset also decides the latitude and longitude used for the calculation of Sun position.

* Vegetation Canopy DSM:
     - A DSM consisting of pixels with vegetation heights above ground. Pixels where no vegetation is present should be set to zero.

* Vegetation Trunk Zone DSM:
     - A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground. Pixels where no vegetation is present should be set to zero.

* Use vegetation DSMs:
     - Tick this box if you want to include vegetation (trees and bushes) when shadows are generated.

* Trunk Zone DSM Exist:
     -  Tick this in if a trunk zone DSM already exist.

* Transmissivity of Light Through Vegetation (%):
     -  Percentage of light that is penetrating through vegetation. Default value is set to 3 % according to Konarska et al. (2013).

* Percent of Canopy Height:
     -  If a trunk zone vegetation DSM is absent, this can be generated based on the height of the Canopy DSM. The default percentage is set to 25%.

* Specify Data:
     -  The data need to be set in the middle section.

* Cast Shadows Only Once:
     -  Tick this box if you only want to cast one shadow. Below this tick box you can set the time that is needed to decide the position of the sun.

* Time Interval between Casting of each Interval:
     -  If the above tick box (Cast shadows only once) is not ticked in, a number of shadows is generated based on the interval set.

* UTC Offset (Hours):
     -  Time zone needs to be specified. Positive numbers moving east(e.g. Stockholm UTC +1).

* Output Folder:
     - A specified folder where the result will be saved.

* Run:
     - Starts the calculations

* Add Results to Project:
     -  If ticked, the shadow raster will be added to the map canvas.

* Close:
     - Closes the plugin.

* Output:
     -  If only one shadow image is generated, one geoTIFF will be produced where pixel values of zero indicates shadow and one indicates sunlit. If daily shadow casting is used (Cast shadows only once ticked off), one shadow image for each time step as well as one shadow fraction image is generated. The shadow fraction image is given in percent where 100% meaning the a pixel is sunlit throughout the day used in the calculation.

* Example of input data and result:
     -  shadow image in Gothenburg (1 m resolution), Sweden at 1 pm on the 2nd of October 2015 (daylight savings time).
            .. figure:: /images/Shadow2.jpg

* Remarks：
            -  All DSMs need to have the same extent and pixel
            -  This plugin is computationally intensive i.e. large grids will take a lot of time and very large grids will not be possible to use. Large grids e.g. larger than 4000000 pixels should be tiled before.


* References ：
      -  Konarska J, Lindberg F, Larsson A, Thorsson S, Holmer B 2013. Transmissivity of solar radiation through crowns of single urban trees—application for outdoor thermal comfort modelling. `Theoret. Appl. Climatol., 1–14 <http://link.springer.com/article/10.1007/s00704-013-1000-3>`__
      -  Lindberg, F., Grimmond, C.S.B., 2011a. The influence of vegetation and building morphology on shadow patterns and mean radiant temperatures in urban areas: model development and evaluation. `Theoret. Appl. Climatol. 105, 311–323 <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
      -  Ratti CF, Richens P (1999) Urban texture analysis with image processing techniques. In: Proceedings of the CAADFutures99, Atalanta, GA


Solar Radiation: Solar Energy on Building Envelopes (SEBE)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
  ::
     Fredrik Lindberg (Gothenburg), Dag Wäsrberg (Tyréns)

* Introduction:
     -  The **SEBE** plugin (Solar Energy on Building Envelopes) can be used to calculate pixel wise potential solar energy using ground and building digital surface models (DSM). SEBE is also able to estimate irradiance on building walls. Optionally, vegetation DSMs could also be used. The methodology that is used to generate irradiance is presented in Lindberg et al. (2015).

* Location:
    - The SEBE plugin is located at
        -  UMEP
          -  Processor
            -  Solar Radiation
              -  Solar Energy on Building Envelopes (SEBE)

* Related Preprocessors ：
          - `MetdataPreprocessor <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_MetPreprocessor>`__, `Download data (WATCH) <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_Download_data_.28WATCH.29>`__, `Wall Height and Aspect <http://www.urban-climate.net/umep/UMEP_Manual#Urban_Geometry:_Wall_Height_and_Aspect>`__

* Dialog box ：
    - Consists of
        -  top section where input data is specified
        -  bottom section for specifying the output and for running the calculations
            .. figure:: /images/SEBE1.png

* Building and Ground DSM:
     - A DSM consisting of ground and building heights. This dataset also decides the latitude and longitude used for the calculation of the Sun position.

* Vegetation Canopy DSM:
     - A DSM consisting of pixels with vegetation heights above ground. Pixels where no vegetation is present should be set to zero.

* Vegetation Trunk Zone DSM:
     - A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground. Pixels where no vegetation is present should be set to zero.

* Use Vegetation DSMs:
     - Tick this box if you want to include vegetation (trees and bushes) into the analysis.

* Trunk Zone DSM Exist:
     -  Tick this in if a trunk zone DSM already exist.

* Transmissivity of Light Through Vegetation (%):
     -  Percentage of light that is penetrating through vegetation. Default value is set to 3 % according to Konarska et al. (2013).

* Percent of Canopy Height:
     -  If a trunk zone vegetation DSM is absent, this can be generated based on the height of the Canopy DSM. The default percentage is set to 25%.

* Wall Height Raster:
     -  A raster of the same size and extent as the ground and building DSM including information of the wall pixels and its height in meters above ground should be specified here. Non wall pixels should be set to zero. This raster is used to estimate irradiance on building walls and can be generated using the Wall Height and Aspect plugin located at UMEP  -> Pre-processing  -> Urban Geometry  -> Wall Height and Aspect.

* Wall Aspect Raster:
     -  A raster of the same size and extent as the ground and building DSM including information of the wall pixels and its aspect, i.e. angle, should be specified here. For example a wall facing towards the south has a value of 180°. Non wall pixels should be set to zero. This raster are used to estimate irradiance on building walls and can be generated using the Wall Height and Aspect plugin located at UMEP  -> Pre-processing  -> Urban Geometry  -> Wall Height and Aspect.

* Albedo:
     -  This parameter specifies the reflectivity of shortwave radiation of all surfaces (ground, roofs, walls and vegetation). It should be a value between 0 and 1. The default value is set to 0.15.

* UTC Offset (Hours):
     -  Time zone needs to be specified. Positive numbers increase when moving east (e.g. Stockholm UTC +1).

* Estimate Diffuse and Direct Shortwave Components from Global Radiation:
     -  Tick this in if only global radiation is present. Diffuse and direct shortwave components will then be estimated from global radiation based on the statistical model presented by Reindl et al. (1990). If air temperature and relative humidity is present, the statistical model will perform better but it is able to estimate the components using only global shortwave radiation.

* Input Meteorological File:
     - Input meteorological data specifically formatted to be used in UMEP. This specific format can be created using UMEP  -> Pre-processing  -> Meteorological data  -> Prepare existing data. A dataset with **hourly** time resolution should be used for SEBE, preferably at least **one year in length**. The time should be in [LST](http://urban-climate.net/umep/UMEP_Manual#Abbreviations) for the specific location to be modelled. Multiple years can also be used to improve the model outcome. Model output is dependent on the meteorological input data so if a short dataset is used, potential solar energy would be valid for that particular time period only.
     - Mandatory data is global shortwave radiation, but the model will perform best if also diffuse and direct components are available.
     - The direct radiation component used as input in the SOLWEIG model is not the direct shortwave radiation on a horizontal surface but on a surface perpendicular to the light source. Hence, the relationship between global radiation and the two separate components are:
          -   Global radiation = direct radiation \* sin(h) + diffuse radiation
          -   where h is the sun altitude. Since diffuse and direct components of short wave radiation is not common data, it is also possible to calculate diffuse and direct shortwave radiation (see above).

* Save Sky Irradiance Distribution:
     -  When the box is ticked in, it is possible to save the radiation distribution from the sky vault calculated from the meteorological file. SEBE first distributes the radiation on 145 sky patches on the sky vault and then generates shadows on the DSMs based on these patches, i.e. the core loop in the model iterates 145 times. For more detailed information on this, see Lindberg et al. (2015).

* Output Folder:
     - A specified folder where result will be saved should be specified here. One raster showing irradiance on ground and building roofs named Energyyearroof.tif is saved as well as a text file of wall irradiance (Energyyearwall.txt). Also, the ground and building DSM is saved in the output folder to be used later in a SEBE visualization plugin (UMEP  -> Post-processing  -> Solar Energy  -> SEBE (Visualisation)).

* Run:
     - This starts the calculations.

* Add Roof and Ground Irradiance Result Raster to Project:
     - If this is ticked in, **Energyyearroof.tif** will be loaded into to the map canvas.

* Close:
     - This button closes the plugin.

* Output:
     -  As mentioned earlier, three mandatory datasets are save is the model was successful. The geoTIFF **Energyyearroof.tif** show pixel wise total irradiance in kWh. **Energyyearwall.txt** show total wall irradiance for each wall column. The column voxel is decided based on the pixel resolution of the input data. Also, the ground and building DSM is saved in the output folder for later use. If the vegetation DSMs were added, one additional file (**Vegetationdata.txt**) including information of vegetation height and location are also saved. This file is also be used in the SBEB visualization plugin.

* Example of input data and result:
     -  Input DSM (left) and irradiance image (right) in Gothenburg using data from 1977.
            .. figure:: /images/SEBE2.jpg

* Remarks：
            -  All DSMs need to have the same extent and pixel
            -  This plugin is computationally intensive i.e. large grids will take a lot of time and very large grids will not be possible to use. Large grids e.g. larger than 4000000 pixels should be tiled before.
* References ：                                                                                                                                                                                                                                                                                                                                                                                                                                                        * References ：
      -  Konarska J, Lindberg F, Larsson A, Thorsson S, Holmer B 2013. Transmissivity of solar radiation through crowns of single urban trees—application for outdoor thermal comfort modelling. Theoret. Appl. Climatol., 1–14 `Link to Paper <http://link.springer.com/article/10.1007/s00704-013-1000-3>`__
      -  Lindberg, F., Jonsson, P. & Honjo, T. and Wästberg, D. (2015) Solar energy on building envelopes - 3D modelling in a 2D environment. Solar Energy. 115 (2015) 369–378 `Link to Paper <http://www.sciencedirect.com/science/article/pii/S0038092X15001164>`__
      -  Reindl DT, Beckman WA, Duffie JA (1990) Diffuse fraction correlation. Sol Energy 45:1–7. `Link to paper <http://www.sciencedirect.com/science/article/pii/0038092X9090060P>`__
