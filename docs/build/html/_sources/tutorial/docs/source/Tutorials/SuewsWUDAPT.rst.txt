.. _SUEWSWUDAPT:

Urban Energy Balance - SUEWS and WUDAPT
=======================================

Introduction
------------

.. note:: This tutorial is not ready for use. Work in progress.

In this tutorial you will generate input data for the 
`SUEWS <http://suews-docs.readthedocs.io>`__ model and simulate spatial 
(and temporal) variations of energy exchanges within an area in New York City using local climate zones derived within the `WUDAPT <http://www.wudapt.org/>`__ project. The World Urban Database and Access Portal Tools project is a community-based project to gather a census of cities around the world.  

Model output may be needed in many formats depending on a users’ needs.
Thus, the format must be useful, while ensuring the science included
within the model is appropriate. The figure below provides an overview of
`UMEP <http://umep-docs.readthedocs.io/en/latest/index.html>`__, a city based climate
service tool (CBCST) used in this tutorial. Within UMEP there are a number 
of models which can predict and diagnose a range of meteorological processes. 

   
   
.. note:: This tutorial is currently designed to work with QGIS 2.18. It is strongly recommended that you goo through the :ref:`SuewsSpatial` tutorial before you go through this tutrial. 


Objectives
----------

To prepare input data for the SUEWS model using a WUDAPT dataset and analyse energy exchanges within an area in New York City.

Steps to be preformed
~~~~~~~~~~~~~~~~~~~~~

#. Download, pre-process the WUDAPT data to create input datasets for the `SUEWS  <http://suews-docs.readthedocs.io>`__ model
#. Run the model
#. Analyse the results


Initial Steps
-------------

UMEP is a python plugin used in conjunction with
`QGIS <http://www.qgis.org>`__. To install the software and the UMEP
plugin see the `getting started <http://umep-docs.readthedocs.io/en/latest/Getting_Started.html>`__ section in the UMEP manual.

As UMEP is under development, some documentation may be missing and/or
there may be instability. Please report any issues or suggestions to our
`repository <https://bitbucket.org/fredrik_ucg/umep/>`__.


Loading and analyzing the spatial data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

All geodata used in this tutorial originates from open datasets available from various sources, foremost from the City of New York. Information about the data is found in the table below.

.. note:: You can download the all the data from `here <https://github.com/Urban-Meteorology-Reading/Urban-Meteorology-Reading.github.io/blob/master/other%20files/SUEWSSpatial_Tutorialdata.zip>`__. Unzip and place in a folder where you have read and write access to.


- Start by loading all the raster datasets into an empty QGIS project. 

The order in the *Layers Panel* decides what layer that will be visible. Here you can also choose not to show a layer in the tick box. You can adjust layers according to your likeing by right-click on a layer in the Layers Panel and choose *Properties*. Note for example that that CDSM (vegetation) is given as height above ground (meter) and that all non-vegetated pixels are set to zero. This makes it hard to get an overview between all 3D objects (buildings and trees).

- Right-click on your **CDSM** layer and go to *Properties > Style* and choose **Singleband pseudocolor** with a min value of 0 and max of 30. Choose also a nice color scheme of your liking.
- Go to *Transparency* and  add and additional no data value of 0. Click ok.
- Now put your **CDSM** layer at the top and your **DSM** layer second in your *Layers Panel*. Now you can see both buislings and vegetation 3D object in your map canvas. 

.. figure:: /images/SUEWSSpatial_dataview.png
   :alt:  none
   :width: 1073px

   DSM and CDSM visible at the same time (click for larger image)

The land cover grid comes with a specific QGIS style file.

- Right-click on the land cover layer (**landcover_2010_nyc**) and choose *Properties*. Down to the left you see a *Style*-button. Choose *Load Style* and open **landcoverstyle.qml** and click OK.
- Make only your land cover class layer visible to examine the spatial variability of the different land cover classes.

The land cover grid has allready been classified into the seven different classes used in most UMEP applications (see table 1). If you have a land cover dataset that is not UMEP formatted you can make use of the *Land Cover Reclassifier* found at *UMEP > Pre-processor > Urban Land Cover > Land Cover Reclassifier* in the menubar to reclassify your data.

Furthermore, a polygon grid (500 m times 500 m) for defining the study area and individual grids are included (Grid_500m.shp). Such grid can be produced directly in QGIS (e.g. *Vector > Research Tools > Vector Grid*) or an external grid can also be used.

- Load the vector layer **Grid_500m.shp** into your QGIS project.
- In the *Style* tab in layer *Properties*, choose a *No Brush* fill style to be able to see the spatial data within each grid.
- Also, add the label IDs for the grid to the map canvas in *Properties > Labels* to make it easier to identify the different grid squares later on in this tutorial. 

As you can see the grid does not cover the whole extent of the raster grids. This is to reduce computation time so that this tutorial will not extent for too long. One grid cell will take approximately 20 seconds to model using SUEWS using meteorological forcing data for a full year.



Preparing input data for the SUEWS model
----------------------------------------

**NOT READY**

One key feature of UMEP is to facilitate the preparation of input data for the various models included. SUEWS requires a number of input information to model the urban energy balance. I plugin called *SUEWS Prepare* has been developed for this purpose. This tutorial make use of high resolution data but there are also possibilities to make use of `WUDAPT <http://www.wudapt.org/>`__ datasets in-conjuction to the *LCZ Converter* (*UMEP > Pre-Processor > Spatial data > LCZ Converter*). 



Population density
~~~~~~~~~~~~~~~~~~
Population density will be used to estimate the anthropogenic heat release (Q\ :sub:`F`) in SUEWS. There is a possibility to make use of both night-time and daytime population densities to make the model more dynamic. You have two different raster grids for night-time (**pop_nighttime_perha**) and daytime (**pop_daytime_perha**), respectively. This time you will make use of a built-in function to QGIS to accuire the population density for each grid.

- Go to *Plugins > Manage and Install Plugins* and make sure that the *Zonal statistics plugin* is ticked in. This is a build-in plugin which comes with the QGIS installation.
- Close the *Plugin maanager* and open *Raster > Zonal Statistics > Zonal Statistics*.
- Choose your **pop_daytime_perha** layer as *Raster layer** and your **Grid_500m** and polygon layer. Use a *Output column prefix* of **PPday** and chose only to calculate *Mean*. Click OK.
- Run the tool again but this time use the night-time dataset.



Running the SUEWS model in UMEP
-------------------------------

To examine energy fluxes for multiple grids, `SUEWSAdvanced` will be used. 

- Open *UMEP > Processor > Urban Energy Balance > SUEWS/BLUEWS, Advanced*. Here you can change some of the run control settings in SUEWS. SUEWS can also be executed outside of UMEP and QGIS (see `SUEWS Manual <http://suews-docs.readthedocs.io>`__. This is recommended when modelling long time series (multiple years) of large model domains (many grid points).
- Leave all the combobox settings at the top as default and tick in both the *Use snow module* and the *Obtain temporal resolution...* box.
- Set the *Temporal resolution of output (minutes) to 60.
- Locate the directory where you save your output from *SUEWSPrepare* earlier and choose an output folder of your choice.
- Click *Run*. This computation will take a while so just have patience. 

Analysing model reults
----------------------

Here I am.
