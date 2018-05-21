Outdoor Thermal Comfort: SOLWEIG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg

* Introduction:
    -  The **SOLWEIG** plugin can be used to calculate spatial variations of mean radiant temperature (T~mrt~) and radiant fluxes using digital surface models (DSM) and ground cover information. Optionally, vegetation DSMs could also be used. The methodology that is used to generate shadows originates from Ratti and Richens (1990) and is further developed and described in Lindberg and Grimmond (2011) and Lindberg et al. (2016). The current version of the model is 2016a.
    -  The full manual of the SOLWEIG model can be found `here <http://urban-climate.net/umep/SOLWEIG>`__.

* Related Preprocessors：
  - `MetPreprocessor`, `WATCH`, `SkyViewFactorCalculator`, `WallHeightandAspect`, `LandCoverReclassifier`

  
* Dialog box：
      .. figure:: /images/SOLWEIG.png

          The dialog for the SOLWEIG model

* Dialog sections ：
.. list-table::
   :widths: 25 75
   :header-rows: 0

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

*  Spatial data：
.. list-table::
   :widths: 25 75
   :header-rows: 0

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
   :widths: 25 75
   :header-rows: 0

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
   :widths: 25 75
   :header-rows: 0

   * - Include POIs
     - By ticking in the option to include POIs (Point of Interest), a vector point layer can be added and full model output are written out to text files for the specific POI. Multiple POIs can be used by including many points in the vector file. See the `full manual <http://www.urban-climate.net/umep/SOLWEIG>`__ for more information.
   * - Adjust sky-emissivity according to Jonsson et al. (2006)
     - Tick this box to include adjustment (0.04) of sky emissivity which was present in the earlier versions of the SOLWEIG model (not recommended).
   * - Consider human as cylinder instead of box
     - Tick this box to consider man as a cylinder instead of a box according to Holmer at al. (2015).

* Environmental parameters：
    Emissivity (ground)||Emissivity of ground. Not used if land cover scheme is activated.
.. list-table::
   :widths: 25 75
   :header-rows: 0

   * - Albedo (buildings)
     - Albedo of building walls and roofs.
   * - Albedo (ground)
     - Albedo of ground surfaces. Not used if land cover scheme is active.
   * - Emissivity (walls)
     - Emissivity of building walls and roofs.
   * - Emissivity (ground)
     - Emissivity of ground. Not used if land cover scheme is activated.

* Human exposure parameters ：
    Posture of the human body||Choose between standing (default) and sitting.

.. list-table::
   :widths: 25 75
   :header-rows: 0

   * - Absorption of shortwave radiation
     - Amount of shortwave radiation that the human body absorb.
   * - Absorption of longwave radiation
     - Amount of longwave radiation that the human body absorb.
   * - Posture of the human body
     - Choose between standing (default) and sitting.


* Output maps:
    A number of different outputs can be chosen here. All grids will be written out as GeoTIFFs at the location specified as the output folder.

* Run:
    Starts the calculations. As SOLWEIG is a 2.5D model, large grids (i.e. high number of pixels) will take a relatively long time to compute. The model is embedded in a so called worker which means that you can continue working with QGIS while the model runs.

* Add Average mean radiant temperature to the map canvas:
    If ticked, an average T\ :sub:`mrt` map will be added to the current

* Close:
    Closes the plugin.

* Quick example on how to run SOLWEIG：
       presented:
             #. Download and extract (unzip) the test dataset (`testdata\_UMEP.zip <https://bitbucket.org/fredrik_ucg/umep/downloads/testdata_UMEP.zip>`__).
             #. Add the raster layers (DSM, CDSM and land cover) from the Goteborg folder into a new QGIS session. The coordinate system of the grids is **Sweref99 1200 (EPSG:3007)**.
             #. In order to run SOLWEIG, some additional datasets must be created based on the raster grids you just added. Open the SkyViewFactor Calculator from the UMEP Pre-processor and calculate SVFs using both your DSM and CDSM. Leave all other settings as default.
             #. Open the Wall height and aspect plugin from the UMEP Pre-processor and calculate both wall height and aspect using the DSM and your input raster. Tick in the box to add them to your project. Leave all other settings as default.
             #. Now you are ready to generate your first T\ :sub:`mrt` map. Open SOLWEIG and use the settings as shown in the figure below but replace the paths to the fit your computer environment. When you are finished, press *Run*.

.. figure:: /images/SOLWEIGfirsttry.png

 Setting for a first try with the SOLWEIG model
 
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
