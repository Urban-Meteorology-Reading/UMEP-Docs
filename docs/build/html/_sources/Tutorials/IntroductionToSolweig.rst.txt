Introduction To Solweig
^^^^^^^^^^^^^^^^^^^^^^^^^



Introduction
------------

In this tutorial you will use a model [SOlar and LongWave Environmental
Irradiance Geometry model (SOLWEIG)] to estimate the mean radiant
temperature (T:sub:`mrt`).

SOLWEIG is a model that simulates spatial variations of 3D radiation
fluxes and the T\ :sub:`mrt` in complex urban settings. It is also able
to model spatial variations of shadow patterns. T\ :sub:`mrt` is one of
the key meteorological variables governing human energy balance and the
thermal comfort of people. It is derived from summing all the radiative
(shortwave and longwave) fluxes (both direct and reflected) to which the
human body is exposed. In SOLWEIG, T\ :sub:`mrt` is derived by modelling
shortwave and longwave radiation fluxes in six directions (upward,
downward and from the four cardinal points) and angular factors.

The model requires **meteorological** forcing data (global shortwave
radiation (K↓), air temperature (T:sub:`a`), relative humidity (RH)),
urban geometry (DSMs), and geographic information (latitude, longitude
and elevation). To determine T\ :sub:`mrt`, continuous maps of sky view
factors are required. Both vegetation and ground cover information can
be added to increase the accuracy of the model output. Below (Figure 1)
a schematic flowchart of SOLWEIG in shown. The `full
manual <http://www.urban-climate.net/umep/SOLWEIG>`__ provides more
detail.

.. figure:: SOLWEIG_flowchart.png
   :alt:  Figure 1: Overview of SOLWEIG

    Figure 1: Overview of SOLWEIG

Objectives
----------

To introduce SOLWEIG and how to run the model within `UMEP (Urban
Multi-scale Environmental
Predictor) <http://urban-climate.net/umep/UMEP_Manual>`__. `Help with
Abbreviations <http://urban-climate.net/umep/UMEP_Manual#Abbreviations>`__

Steps
~~~~~

#. Generation of the different kinds of input data that are needed to
   run the model
#. How to run the model
#. How to examine the model output
#. Add additional information (vegetation and ground cover) to improve
   the model outcome and to examine the effect of climate sensitive
   design

Initial Practical steps
-----------------------

UMEP is a python plugin used in conjunction with
`QGIS <http://www.qgis.org>`__. To install the software and the UMEP
plugin see the `getting
started <http://urban-climate.net/umep/UMEP_Manual#Getting_Started>`__
section in the UMEP manual.

As UMEP is under constant development, some documentation may be missing
and/or there may be instability. Please report any issues or suggestions
to our `repository <https://bitbucket.org/fredrik_ucg/umep/>`__.

Data for this exercise
~~~~~~~~~~~~~~~~~~~~~~

To make use of the datasets a (for `password access is
required <http://urban-climate.net/umep/UMEP_Manual#Tutorials>`__) The
UMEP tutorial datasets can be downloaded from our here
`Goteborg\_SWEREF99\_1200.zip <http://www.urban-climate.net/UMEPTutorials/Gothenburg/Goteborg_SWEREF99_1200.zip>`__

-  Download, extract and add the raster layers (DSM, CDSM, DEM and land
   cover) from the **Goteborg folder** into a new QGIS session (see
   below).

   -  Create a new project
   -  Examine the geodata by adding the layers (*DSM\_KRbig*,
      *CDSM\_KRbig*, *DEM\_KRbig* and *landcover*) to your project
      (`Layer > Add Layer > Add Raster
      Layer <Media:Add_Raster_Layer.png>`__).

-  Coordinate system of the grids is Sweref99 1200 (EPSG:3007). If you
   look at the lower right hand side you can see the CRS used in the
   `current QGIS project <Media:GOT_LUP.png>`__
-  Examine the different datasets before you move on.

-  To add a legend to the **land cover** raster you can load
   **landcoverstyle.qml** found in the test dataset. Right click on the
   land cover (*Properties -> Style (lower left) -> Load Style*).

SOLWEIG Model Inputs
--------------------

Details of the model inputs and outputs are provided in the `SOLWEIG
manual <http://urban-climate.net/umep/SOLWEIG>`__. As this tutorial is
concerned with a **simple application** only the most critical
parameters are used. Many other parameters can be modified to more
appropriate values if applicable. The table below provides an overview
of the parameters that can be modified in the Simple application of
SOLWEIG.

-  R: required O: Optional N : not needed

+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Type                                                                     | Definition                                                                                   | Use   | Reference/Comments                                                                                                                       |
+==========================================================================+==============================================================================================+=======+==========================================================================================================================================+
| **Spatial data**                                                         |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Ground and building DSM (DSDM)                                           | High resolution surface model of ground and building heights                                 | R     | Given in metres above sea level (m asl)                                                                                                  |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Digital elevation model (DEM)                                            | High resolution surface model of the ground                                                  | R\*   | R\* if land cover is absent to identify buildings. Given in m asl. Must be same resolution as the DSM.                                   |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Digital canopy surface model (CDSM)                                      | High resolution surface model of 3D vegetation                                               | O     | Given in metres above ground level (m agl). Must be same resolution as the DSM.                                                          |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Digital trunk zone surface model (TDSM)                                  | High resolution surface model of trunk zone heights (underneath tree canopy)                 | O     | Given in m agl. Must be same resolution as the DSM.                                                                                      |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Land (ground) cover information (LC)                                     | High resolution surface model of ground cover                                                | O     | Must be same resolution as the DSM. Five different ground covers are currently available (building, paved, grass, bare soil and water)   |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| **Meteorological data**                                                  |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| UMEP formatted meteorological data                                       | Meteorological data from one nearby observation station, preferably at 1-2 m above ground.   | R     | Any time resolution can be given.                                                                                                        |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| **Other**                                                                |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Latitude (°)                                                             | Solar related calculations                                                                   | R     | Obtained from the ground and building CRS                                                                                                |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Longitude (°)                                                            | Solar related calculations                                                                   | R     | Obtained from the ground and building CRS                                                                                                |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| `UTC (h) <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`__   | Time zone                                                                                    | R     | Influences solar related calculations. Set in the interface of the model.                                                                |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Human exposure parameters                                                | Absorption of radiation and posture                                                          | R     | Set in the interface of the model.                                                                                                       |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
| Environmental parameters                                                 | e.g. albedos and emissivites of surrounding urban fabrics                                    | R     | Set in the interface of the model.                                                                                                       |
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+
+--------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+-------+------------------------------------------------------------------------------------------------------------------------------------------+

Meterological input data should be in UMEP format. You can use the
`Meterological
Preprocessor <http://www.urban-climate.net/umep/UMEP_Manual#Meteorological_Data:_MetPreprocessor>`__
to prepare your input data. There is also a possibility to use a single
point in time in the plugin.

-  R: required O: Optional N : not needed

+-------+-------+---------------+------------------------------------------------------------------------------+
| No.   | USE   | Column name   | Description                                                                  |
+=======+=======+===============+==============================================================================+
| 1     | R     | iy            | Year [YYYY]                                                                  |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 2     | R     | id            | Day of year [DOY]                                                            |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 3     | R     | it            | Hour [H]                                                                     |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 4     | R     | imin          | Minute [M]                                                                   |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 5     | N     | qn            | Net all-wave radiation [W m\ :sup:`-2`]                                      |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 6     | N     | qh            | Sensible heat flux [W m\ :sup:`-2`]                                          |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 7     | N     | qe            | Latent heat flux [W m\ :sup:`-2`]                                            |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 8     | N     | qs            | Storage heat flux [W m\ :sup:`-2`]                                           |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 9     | N     | qf            | Anthropogenic heat flux [W m\ :sup:`-2`]                                     |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 10    | N     | U             | Wind speed [m s\ :sup:`-1`]                                                  |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 11    | R     | RH            | Relative Humidity [%]                                                        |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 12    | R     | Tair          | Air temperature [°C]                                                         |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 13    | O     | pres          | Barometric pressure [kPa]                                                    |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 14    | N     | rain          | Rainfall [mm]                                                                |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 15    | R     | kdown         | Incoming shortwave radiation [W m\ :sup:`-2`] Must be >= 0 W m\ :sup:`-2`.   |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 16    | N     | snow          | Snow [mm]                                                                    |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 17    | N     | ldown         | Incoming longwave radiation [W m\ :sup:`-2`]                                 |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 18    | N     | fcld          | Cloud fraction [tenths]                                                      |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 19    | N     | Wuh           | External water use [m:sup:`3`]                                               |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 20    | N     | xsmd          | Observed soil moisture [m3 m\ :sup:`-3` or kg kg\ :sup:`-1`]                 |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 21    | N     | lai           | Observed leaf area index [m2 m\ :sup:`-2`]                                   |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 22    | O     | kdiff         | Diffuse radiation [W m\ :sup:`-2`]                                           |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 23    | O     | kdir          | Direct radiation [W m\ :sup:`-2`]                                            |
+-------+-------+---------------+------------------------------------------------------------------------------+
| 24    | N     | wdir          | Wind direction [°]                                                           |
+-------+-------+---------------+------------------------------------------------------------------------------+

How to Run SOLWEIG from the UMEP-plugin
---------------------------------------

#. Open SOLWEIG from *UMEP -> Processor -> Outdoor Thermal Comfort ->
   Mean radiant temperature (SOLWEIG)*.

   -  Some additional information about the plugin is found in the lower
      left window. You will make use of a test dataset from observations
      for Gothenburg, Sweden. |Figure 2: Dialog for the SOLWEIG model|

#. To be able to run the model some additional spatial datasets needs to
   be created.

   -  Close the SOLWEIG plugin and open *UMEP -> Pre-Processor -> Urban
      geometry -> Sky View Factor*.
   -  To run SOLWEIG various sky view factor (SVF) maps for both
      vegetation and buildings must be created (see `Lindberg and
      Grimmond
      (2011) <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
      for details).
   -  You can create all SVFs needed (vegetation and buildings) at the
      same time. Use the settings as shown below. Use an appropriate
      output folder for your computer. |Figure 3: Settings for the
      SkyViewFactorCalculator.|
   -  When the calculation is done, map will appear in the map canvas.
      This is the 'total' SVF i.e., including both buildings and
      vegetation. Examine the dataset.
   -  Where are the highest and lowest values found?
   -  Look in your output folder and find a zip-file containing all the
      necessary SVF maps needed to run the SOLWEIG-model.

#. Another preprocessing plugin needed is to create the building wall
   heights and aspect. Open *UMEP -> Pre-Processor -> Urban geometry ->
   Wall height and aspect* and use the settings as shown below (Figure
   4).\ |Figure 4: Settings for the Wall height and aspect plugin.|
#. Re-open the SOLWEIG plugin and use the settings (Figure 5). You will
   use the GUI to set one point in time (i.e. a summer hour in
   Gothenburg, Sweden) hence, no input meteorological file is needed for
   now. No information on vegetation and ground cover is added for this
   first try. Click **Run**. |Figure 5: The settings for your first
   SOLWEIG run.|
#. Examine the output (Average T\ :sub:`mrt` [°C]. What is the main
   driver to the spatial variations in T\ :sub:`mrt`?
#. Add 3D vegetation information by ticking in *Use vegetation scheme
   (Lindberg, Grimmond 2011)* and add **CDSM\_Krbig** as the *Vegetation
   Canopy DSM*. As no TDSM exists we estimate the it by using 25% of the
   canopy height. Leave the tranmissivity as 3%. Tick in *Save generated
   Trunk Zone DSM* (a tif file, **TDSM.tif**, will be generated in the
   specified output folder and used in a later section: **Climate
   sensitive planning**). Also tick in *Save generated building grid* as
   this will be needed later in this tutorial. Leave the other setting
   as before (Step 4) except for changing your output directory
   Otherwise, results from your first run will be overwritten. Run the
   model again and compare the result with your first run.
#. Add your last spatial dataset, the **land cover** grid by ticking in
   *Use land cover scheme (Lindberg et al. 2016)*. Run and compare the
   result again with the previous runs.

Using meteorolgical data and POIs
---------------------------------

SOLWEIG is also able to run a continuous dataset of meteorological data.
You will make use of a single summer day as well as a winter day for
Gothenburg, Sweden. The GUI is also able to derive full model output
(all calculated variables) from certain points of interest (POIs).

#. First you need to create a point vector layer to store the POIs. Go
   to *Layer -> Create Layer -> New Shape file*. Choose *Point* as
   *Type* and add a new text field called **name**. Name the new layer
   **POI\_Kr.shp**. Specify the coordinate system as SWEREF99 12 00
   (EPSG: 3007).
#. Now you should add two points within the study area. To add points to
   the layer it has to be editable and Add Feature should be activated
   (Figure 6). |Figure 6: Setting to add points| Two points should be
   added and the attributes should be id=\ **1** and
   name=\ **courtyard** for the right point and id=\ **2** and
   name=\ **park** for the left point. See Figure 7 for the locations of
   the two points. |Figure 7: Location of the two POIs| When you are
   finished, save layer edits (box in-between the two marked boxes in
   Figure 6). Close the editing by pressing Toggle editing (the pencil).
#. Now open the SOLWEIG plugin. Use both the vegetation and land cover
   schemes as before. This time, tick in *Include POI(s)*, select your
   point layer and use the ID attribute as *ID field*.
#. Tick in *Use continuous meteorological dataset* and choose
   **gbg19970606\_2015a.txt** as *Input meteorological file*. Also, tick
   in to save T\ :sub:`mrt` as *Output maps*. Run the model again.

Examine your output with SOLWEIG Analyzer
-----------------------------------------

To perform a first set of analysis of your result you can make use of
the SOLWEIG Analyzer plug-in.

#. Open the Analyzer located in *UMEP -> Post-Processor -> Outdoor
   Thermal Comfort -> SOLWEIG Analyzer*. Here you can analyze both data
   from your POIs as well as perform statistical analysis based on saved
   output maps. Start by locating your output folder in the top section
   (*Load Model Result*). |Figure 2: Dialog for the SOLWEIG Analyzer
   plug-in|
#. Firstly you will compare differences in T\ :sub:`mrt` for the two
   locations (courtyard and park). This can done using the left frame
   (*Point of Interest data*). Specify *courtyard* as *POI* and *Mean
   Radiant Temperature* in the two top scroll down lists. Then tick in
   *Include another POI/variable* and chose *park* and *Mean Radiant
   Temperature* below. Click *Plot*. What explains the differences?
#. Now lets us move on to analyse the output maps generated from our
   last model run. In the right frame, specify *Mean Radiant
   Temperature* as *Variable to visualize*. Start by clicking *Show
   Animation*. Now the output maps of T\ :sub:`mrt` generated before are
   displayed in a sequence.
#. Next step is to generate some statistical maps from the last model
   run. Specify *Mean Radiant Temperature* as *Variable to visualize*
   and tick in to *Exclude building pixels*. Choose the building grid
   that you saved earlier in this tutorial. If it is not in the
   drop-down list you need to add this layer (**buildings**) to your
   project. Tick in *T\ :sub:`mrt`: Percent of time above threshold
   (degC)* and specify 55.0 as threshold. Specify an output folder and
   tick also in *Add analysis to map canvas* before you generate the
   result. The resulting map show the time that a pixel has been above
   55 degC based on the whole analysis time i.e. 24 hours. This type of
   maps can be used to identify areas prone to e.g. heat stress

Climate sensitive planning
--------------------------

Vegetation is one effective measure to reduce areas prone to heat
related health issues. In this section you make use of the Tree
Generator plugin to see the effect of adding more vegetation into our
study area. The municipality in Gothenburg have identified a “hot spot”
south of the german church and they want to see the effect of planting
three new trees in that area.

The Tree Generator
~~~~~~~~~~~~~~~~~~

The Tree Generator plugin make use of a point vector file including the
necessary attributes to generate/add/remove vegetation suitable for
either mean radiant temperature modelling with SOLWEIG or urban energy
balance modelling with SUEWS.

#. Create a point vector shape file named (**TreesKR.shp**) as described
   in the previous section adding five attributes (*id, ttype, trunk,
   totheight, diameter*). The attributes should all be decimal (float)
   numbers (see table below). The location of the three new trees are
   shown in Figure 8. The values for all three vegetation units should
   be **ttype=2, trunk=4, totheight=15, diameter=10**. |Figure 8:
   Location of the three new vegetation units|.
#. Add your created trunk zone dsm (TDSM.tif) that was created
   previously (located in your output directory).
#. Open the TreeGenerator (UMEP -> PreProcessor -> TreeGenerator) and
   use the settings as shown in Figure 9. |Figure 9: The settings for
   the Tree Generator|
#. As the vegetation DSMs have been changed, the SVFs has to be
   recalculated. This time use the two generated vegetation DSMs.
#. Now re-run SOLWEIG using the same settings as before but now use the
   new vegetation surface models as well as the new SVFs generated in
   the previous step.
#. Generate a new, updated threshold map based on the new results and
   compare the differences.

The table below show the input variables needed for each tree point.

+------------------+-----------------------------+--------------------------------------------+
| Attribute name   | Name                        | Description                                |
+==================+=============================+============================================+
| ttype            | Tree type                   | Two shapes are available:                  |
|                  |                             |                                            |
|                  |                             | -  conifer = 1 and                         |
|                  |                             | -  deciduous = 2.                          |
|                  |                             | -  To remove vegetation set ttype = 0.     |
+------------------+-----------------------------+--------------------------------------------+
| trunk            | Trunk zone height (m agl)   | Height of the trunk zone.                  |
+------------------+-----------------------------+--------------------------------------------+
| totheight        | Total tree height (m agl)   | Maximum height of the vegetation unit      |
+------------------+-----------------------------+--------------------------------------------+
| diameter         | Canopy diameter (m)         | Circular diameter of the vegetation unit   |
+------------------+-----------------------------+--------------------------------------------+

.. |Figure 2: Dialog for the SOLWEIG model| image:: SOLWEIG.png
.. |Figure 3: Settings for the SkyViewFactorCalculator.| image:: Svf_solweig.png
.. |Figure 4: Settings for the Wall height and aspect plugin.| image:: Wall_solweig.png
.. |Figure 5: The settings for your first SOLWEIG run.| image:: Tmrt1_solweig.png
.. |Figure 6: Setting to add points| image:: Addpoint.png
.. |Figure 7: Location of the two POIs| image:: Pointskr.png
.. |Figure 2: Dialog for the SOLWEIG Analyzer plug-in| image:: SOLWEIGAnalyzer.png
.. |Figure 8: Location of the three new vegetation units| image:: TreesKR.png
.. |Figure 9: The settings for the Tree Generator| image:: Treegeneratorsolweig.png
