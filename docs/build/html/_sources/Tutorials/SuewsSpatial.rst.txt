.. _SuewsSpatial:

SUEWS Spatial
=============

Introduction
------------

In this tutorial you will generate input data to the 
`SUEWS <http://urban-climate.net/umep/SUEWS>`__ model and simulate spatial 
(and temporal) variations of energy exchanges within a small area on Manhattan 
(New York City) with regards to a heat wave event. 

Tools such as this, once appropriately assessed for an area, can be used
for a broad range of applications. For example, for climate services
(e.g. http://www.wmo.int/gfcs/). Running a model can allow analyses,
assessments, and long-term projections and scenarios. Most applications
require not only meteorological data but also information about the
activities that occur in the area of interest (e.g. agriculture,
population, road and infrastructure, and socio-economic variables).

Model output may be needed in many formats depending on a users’ needs.
Thus, the format must be useful, while ensuring the science included
within the model is appropriate. Figure 1 provides an overview of
`UMEP <http://urban-climate.net/umep/UMEP>`__, a city based climate
service tool (CBCST) used in this tutorial. Within UMEP there are a number 
of models which can predict and diagnose a range of meteorological processes. 

.. figure:: /images/SUEWSIntro_UMEP_overview.png
   :alt:  none
   :width: 378px

   Figure 1: Overview of the climate service tool UMEP (from Lindberg et al. 2018)
   
   
.. note:: This tutorial is currently designed to work with QGIS 2.18. It is recommended that you have a look at the tutorials :ref:`IntroductionToSuews` and :ref:`SuewsAdvanced` before you go through this tutrial. 


Objectives
----------

To perform and analyse energy exchanges within a small area on Manhattan, NYC.

Steps to be preformed
~~~~~~~~~~~~~~~~~~~~~

#. Pre-process the data and create input datasets for the SUEWS model
#. Run the model
#. Analyse the results
#. Perform simple mitigation measures to see how it affects the model results (optional)


Initial Steps
-------------

UMEP is a python plugin used in conjunction with
`QGIS <http://www.qgis.org>`__. To install the software and the UMEP
plugin see the `getting
started <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__
section in the UMEP manual.

As UMEP is under development, some documentation may be missing and/or
there may be instability. Please report any issues or suggestions to our
`repository <https://bitbucket.org/fredrik_ucg/umep/>`__.


Loading and analyzing the spatial data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All geodata used in this tutorial originates from open datasets available from various sources, foremost from the City of New York. Information about the data is found in table 1.

.. note:: You can download the all the data from **here (NEED TO BE FIXED)**. Unzip and place in a folder where you have read and write access.

.. list-table:: Table 1. Spatial data used for this tuorial
   :widths: 10 10 40 40

   * - **Geodata**
     - **Year**
     - **Source**
     - **Description**
   * - Digital surface model (DSM)
     - 2013 (Lidar), 2016 (building polygons)
     - United States Geological Survey (USGS). New York CMGP Sandy 0.7m NPS Lidar and NYC Open Data Portal. `link <https://data.cityofnewyork.us>`__
     - A raster grid including both buildings and ground given in meter above sea level.
   * - Digital elevation model (DEM)
     - 2013
     - United States Geological Survey (USGS). New York CMGP Sandy 0.7m NPS Lidar. `link <https://data.cityofnewyork.us>`__	
     - A raster grid including only ground heights given in meter above sea level.
   * - Digital canopy model (CDSM)
     - 2013 (August)
     - United States Geological Survey (USGS). New York CMGP Sandy 0.7m NPS Lidar. `link <https://coast.noaa.gov/htdata/lidar1_z/geoid12b/data/4920/>`__
     - A vegetation raster grid where vegetation heights is given in meter above ground level. Vegetation lower than 2.5 meter Pixels with no vegetation should be zero.
   * - Land cover (UMEP formatted)
     - 2010
     - New York City Landcover 2010 (3ft version). University of Vermont Spatial Analysis Laboratory and New York City Urban Field Station. `link <https://opendata.cityofnewyork.us/>`__
     - A raster grid including: 1. Paved surfaces, 2. Building surfaces, 3. Evergreen trees and shrubs, 4. Deciduous trees and shrubs, 5. Grass surfaces, 6. Bare soil, 7. Open water			
   * - Population density (residential)
     - 2010
     - 2010 NYC Population by Census Tracts, Department of City Planning (DCP). `link <https://data.cityofnewyork.us>`__)
     - People per census tract converted to pp/ha. Converted from vector to raster.
   * - Land use
     - 2018
     - NYC Department of City Planning, Technical Review Division. `link <https://zola.planning.nyc.gov>`__
     - Used to redistribute population during daytime (see text). Converted from vector to raster	 			
	
	
- Start by loading all the raster datasets into an empty QGIS project. 

The order in the *Layers Panel* decides what layer that will be visible. Here you can also choose not to show a layer in the tick box. You can adjust layers according to your likeing by right-click on a layer in the Layers Panel and choose *Properties*. Note for example that that CDSM (vegetation) is given as height above ground (meter) and that all non-vegetated pixels are set to zero. This makes it hard to get an overview between all 3D objects (buildings and trees).

- Right-click on your **CDSM** layer and go to *Properties > Style* and choose **Singleband pseudocolor** with a min value of 0 and max of 30. Choose also a nice color scheme of your liking.
- Go to *Transparency* and  add and additional no data value of 0. Click ok.
- Now put your **CDSM** layer at the top and your **DSM** layer second in your *Layers Panel*. Now you can see both buislings and vegetation 3D object in your map canvas (Figure 2). 

.. figure:: /images/SUEWSSpatial_dataview.png
   :alt:  none
   :width: 1073px

   Figure 2: DSM and CDSM visible at the same time (click for larger image)

The land cover grid comes with a specific QGIS style file.

- Right-click on the land cover layer (**landcover_2010_nyc**) and choose *Properties*. Down to the left you see a *Style*-button. Choose *Load Style* and open **landcoverstyle.qml** and click OK.
- Make only your land cover class layer visible to examine the spatial variability of the different land cover classes.

The land cover grid has allready been classified into the seven different classes used in most UMEP applications (see table 1). If you have a land cover dataset that is not UMEP formatted you can make use of the *Land Cover Reclassifier* found at *UMEP > Pre-processor > Urban Land Cover > Land Cover Reclassifier* in the menubar to reclassify your data.

Furthermore, a polygon grid (500 m times 500 m) for defining the study area and individual grids are included (Grid_500m.shp). Such grid can be produced directly in QGIS (e.g. *Vector > Research Tools > Vector Grid*) or an external grid can also be used.

- Load the vector layer **Grid_500m.shp** into your QGIS project.
- In the *Style* tab in layer *Properties*, choose a *No Brush* fill style to be able to see the spatial data within each grid.
- Also, add the label IDs for the grid to the map canvas in *Properties > Labels* to make it easier to identify the different grid squares later on in this tutorial. 

As you can see the grid does not cover the whole extent of the raster grids. This is to reduce computation time so that this tutorial will not extent for too long. One grid cell will take approximately 20 seconds to model using SUEWS using meteorological forcing data for a full year.

Meteorlogical forcing data
~~~~~~~~~~~~~~~~~~~~~~~~~~

NOT READY. Depends on if WATCH will be used or not.


Preparing input data for the SUEWS model
----------------------------------------

One key feature of UMEP is to facilitate the preparation of input data for the various models included. SUEWS requires a number of input information to model the urban energy balance. I plugin called *SUEWS Prepare* has been developed for this purpose. This tutorial make use of high resolution data but there are also possibilities to make use of `WUDAPT <http://www.wudapt.org/>`__ datasets in-conjuction to the *LCZ Converter* (*UMEP > Pre-Processor > Spatial data > LCZ Converter*). 

- Open SUEWS Prepare (*UMEP > Pre-Processor > SUEWS prepare*)

.. figure:: /images/SUEWSSpatial_Prepare1.png
   :alt:  none
   :width: 1173px

   Figure 3: The *SUEWS Prepare* plugin (click for a larger image).

Here you can see all the various settings that can be made. You will focus on the *Main Settings* tab where the mandatory settings are made. The other tabs include the settings for e.g. different land cover classes, human activities etc.

There are 10 frames included in the *Main Settings* tab where 8 need to be filled in for this tutorial:

#. **Polygon grid**
#. **Building morphology**
#. **Tree morphology**
#. **Land cover fractions**
#. **Meteorological data** 
#. **Population density**
#. **Daylight savings and UTC**
#. **Initial conditions**

The two optional frames (*Land use fractions* and *Wall area*) should be used if the ESTM model should be used which is a model scheme used to estimate the storage energy term (Q\ :sub:`S`). You will use another modelling scheme (*OHM*) and therefore, these two tabs could be ignored for now.

- Close *SUEWS Prepare*

Building morphology
~~~~~~~~~~~~~~~~~~~
First you will calculate roughness paprmeters based on the building geometry within your grids.

- Open *UMEP > Pre-Processor > Urban Morphology > Morphometric Calculator (Grid)*.
- Use the settings in Figure 4 and press *Run*.
- When calculation ids done, close the plugin.

.. figure:: /images/SUEWSSpatial_IMCGBuilding.png
   :alt:  none

   Figure 4: The settings for calculating building morphology.

This operation should have produced 17 different text files; 16 (*anisotrophic*) that include morphometric parameters from each 5 degree section for each grid and one file (*isotropic*) that includes averaged values for each of the 16 grids. You can open **build_IMPGrid_isotropic.txt** and compare the different values for a park grid (3054) and an urban grid (3242). Header abbreviations is explained **here** (**LINK NOT READY**).

Tree morphology
~~~~~~~~~~~~~~~
Now you will calculate roughness paprmeters based on the vegetation (trees and bushes) within your grids. As you noticed there is only one surface data for vegetation present (**CDSM_nyc**) and if you examine your land cover grid (**landcover_2010_nyc**) you can see that there is only one class of high vegetation (*Deciduous trees*) present with our model domain. Therefore, you will not separate between evergreen and deciduous vegetation in this tutorial. As shown in table 1, the tree surface model represents height above ground.

- Again, Open *UMEP > Pre-Processor > Urban Morphology > Morphometric Calculator (Grid)*.
- Use the settings in Figure 5 and press *Run*.
- When calculation ids done, close the plugin.

.. figure:: /images/SUEWSSpatial_IMCGVeg.png
   :alt:  none

   Figure 5: The settings for calculating vegetation morphology.

Land cover fractions
~~~~~~~~~~~~~~~~~~~~
Moving on to land cover fraction calculations for each grid.

- Open *UMEP > Pre-Processor > Urban Land Cover > Land Cover Fraction (Grid)*.
- Use the settings in Figure 6 and press *Run*.
- When calculation ids done, close the plugin.

.. figure:: /images/SUEWSSpatial_LCF.png
   :alt:  none

   Figure 6: The settings for calculating land cover fractions

Population density
~~~~~~~~~~~~~~~~~~
Population density will be used to estimate the anthropogenic heat release (Q\ :sub:`F`) in SUEWS. There is a possibility to make use of both night-time and daytime population densities to make the model more dynamic. You have two different raster grids for night-time (**pop_nighttime_perha**) and daytime (**pop_daytime_perha**), respectively. This time you will make use of a built-in function to QGIS to accuire the population density for each grid.

- Go to *Plugins > Manage and Install Plugins* and make sure that the *Zonal statistics plugin* is ticked in. This is a build-in plugin which comes with the QGIS installation.
- Close the *Plugin maanager* and open *Raster > Zonal Statistics > Zonal Statistics*.
- Choose your **pop_daytime_perha** layer as *Raster layer** and your **Grid_500m** and polygon layer. Use a *Output column prefix* of **PPday** and chose only to calculate *Mean*. Click OK.
- Run the tool again but this time use the night-time dataset.

SUEWS Prepare
~~~~~~~~~~~~~
Now you are ready to organise all input data into the SUEWS input format.

- Open *SUEWS Prepare*
- In the *Polygon grid* frams, choose your polygon grid (**Grid_500m**) and choose **id** as your *ID field*
- In the *Building morphology* frame, fetch the file called **build_IMPGrid_isotropic.txt**.
- In the *Land cover fractions* frame, fetch the file called **lc_LCFG_isotropic.txt**.
- In the *Tree morphology* frame, fetch the file called **veg_IMPGrid_isotropic.txt**.
- In the *Meteorological data* frame, fetch your UMEP formatted met forcing data text file.
- In the *Population density* frame, choose the appropriate attributes created in the previous section for daytime and night-time population density.
- In the *Daylight savings and UTC* frame, leave start and end of the daylight saving as they are and choose *-5*.
- In the *Initial conditions* frame, choose **Winter (0%)** in the *Leaf Cycle*, 100% *Soil moisture state* and **nyc** as a *File code**.
- Choose an empty directory as your *Output folder*.
- Press *Generate*
- When processing is finished, close *SUEWS Prepare*.

Running the SUEWS model in UMEP
-------------------------------

Here er jag...
