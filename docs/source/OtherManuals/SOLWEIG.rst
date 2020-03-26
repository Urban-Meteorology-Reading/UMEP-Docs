.. _SOLWEIGManual:

SOLWEIG Manual
--------------

The current version of SOLWEIG is v2019a (released 22 May 2019).

NEW in this version: see `Version History`_.

The manual for SOLWEIG should be referenced as follows:

*F Lindberg, CSB Grimmond 2019. SOLWEIG_v2018a Department of Earth Sciences, University of Gothenburg, Sweden, University of Reading, UK.*

Introduction
~~~~~~~~~~~~

SOLWEIG is a model which can be used to estimate spatial variations of
3D radiation fluxes and mean radiant temperature (|TMRT|) in
complex urban settings. The SOLWEIG model follows the same approach
commonly adopted to observe T\ :sub:`mrt` (as used, for example, by
Höppe (1992)  [1]_, with shortwave and longwave radiation fluxes from
six directions being individually calculated to derive T\ :sub:`mrt`.
The model requires a limited number of inputs, such as direct, diffuse
and global shortwave radiation, air temperature, relative humidity,
urban geometry and geographical information (latitude, longitude and
elevation). Additional vegetation and ground cover information can also
be used to imporove the estimation of T\ :sub:`mrt`. Below is a
flowchart of the model.

.. figure:: /images/SOLWEIG_flowchart.png
   :align: center
   :alt:  Overview of SOLWEIG

   Overview of SOLWEIG

Suggested reading
^^^^^^^^^^^^^^^^^

Read the manual and papers listed below to get a full explanation of the
model and previous evaluation:

-  Lindberg, F., Onomura, S. and Grimmond, C.S.B (2016) Influence of
   ground surface characteristics on the mean radiant temperature in
   urban areas. International Journal of Biometeorology. 60(9),
   1439-1452. (`link to
   paper <http://link.springer.com/article/10.1007/s00484-016-1135-x>`__)
-  Lindberg, F. and Grimmond, C. (2011) The influence of vegetation and
   building morphology on shadow patterns and mean radiant temperature
   in urban areas: model development and evaluation. Theoretical and
   Applied Climatology 105:3, 311-323. (`link to
   paper <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__)
-  Lindberg, F., Holmer, B. and Thorsson, S. (2008) SOLWEIG 1.0 –
   Modelling spatial variations of 3D radiant fluxes and mean radiant
   temperature in complex urban settings. International Journal of
   Biometeorology 52, 697–713. (`link to
   paper <http://link.springer.com/article/10.1007/s00484-008-0162-7>`__)
-  Holmer, B., Lindberg, F., Rayner, D. and Thorsson, S. (2015) How to
   transform the standing man from a box to a cylinder – a modified
   methodology to calculate mean radiant temperature in field studies
   and models, ICUC9 – 9 th International Conference on Urban Climate
   jointly with 12th Symposium on the Urban Environment, BPH5: Human
   perception and new indicators. Toulouse, July 2015. (`link to
   paper <http://www.meteo.fr/icuc9/LongAbstracts/bph5-2-3271344_a.pdf>`__)

Install the model
^^^^^^^^^^^^^^^^^

As SOLWEIG is included in UMEP (as from version 0.2.1) follow the
`Getting_Started`
on how to install QGIS and UMEP. When installed successfully, SOLWEIG is
found under *UMEP -> Processor -> Outdoor Thermal Comfort -> Mean
Radiant Temperature (SOLWEIG)*.

Input data
~~~~~~~~~~

There are two categories of data needed to run SOLWEIG. The first
category is the spatial information in the some various raster grids
explained below. The other is meteorological data and other settings
such as environmental and human exposure parameters.

Surface models
^^^^^^^^^^^^^^

One essential prerequisite for performing successful model calculation
is that all surface models are of the same extent and pixel resolution.

Ground and building DSM
#######################

As the name suggest this DSM consist of both ground and building heights
(masl).

Vegetation DSMs
###############

3D Vegetation is described by two different grids. First a canopy DSM
(CDSM) which represents the top of the vegetation and second, a trunk
zone DSM (TDSM) that describes the bottom of the vegetation (see
schematic figure). Pixel without any 3D vegetation has the value of zero
and vegetation pixels are given in magl. For a detailed description, see
Lindberg and Grimmond (2011)  [2]_.

.. figure:: /images/Vegdems.png
   :align: center
   :alt: Schematic cross section of the vegetation representation in SOLWEIG. a Conifer tree (left) and bush (right), b the canopy DEM and c trunk zone DEM based on (a). From Lindberg and Grimmond (2011)

   Schematic cross section of the vegetation representation in SOLWEIG.
   **a** Conifer tree (left) and bush (right), **b** the canopy DEM and
   **c** trunk zone DEM based on (a). From Lindberg and Grimmond (2011)

.. figure:: /images/Dsm_gbg.png
    :align: center

    Example of a ground and building DSM


Digital elevation model
#######################

One essential information needed is to know what pixels that are
occupied with buildings. In order to locate these pixels, there are two
possible ways:

#. By including a DEM which can bu used in conjunction with the ground
   and building DSM to derive building pixels.
#. By using a land cover grid (see below) where buildings are
   represented.

If a DEM is used, is has to be the same spatial resolution and extent as
all the other grids used.

Ground cover grid
#################

If the ground cover scheme as presented in Lindberg et al. (2016)  [3]_
should be used, a ground cover grid should be included. The Ground cover
grid should be in the UMEP standard format **except** for the two tree
classes (deciduous and conifer). In other words a ground cover grid in
SOLWEIG represents what is on the ground surface. A UMEP ground cover
grid can be prepared from other data using the Land Cover Reclassifier
(*UMEP -> Pre-Processor ->* `LandCoverReclassifier`)

Meteorological data
^^^^^^^^^^^^^^^^^^^

The format and variables used for meteorological data is the same as for
other parts of the UMEP-plugin. The time resolution is optional. To
prepare such dataset from existing data the `Metdata
Preprocessor <MetPreprocessor>`
could be used. If no data is available a single point in time can
modelled using the SOLWEIG interface. There is also a possibility to
download a dataset for any location on Earth using the `Download data
(WATCH) <WATCH>`-plugin.
The variables required for SOLWIEG are:

-  *Air temperature* [degC]
-  *Relative humidity* [%]
-  *Incoming shortwave radiation* [W m\ :sup:`-2`]

Required are also the components of *diffuse* and *direct* shortwave
radiation. If these are unavailable, and submodel developed by Reindl et
al. (1990)  [4]_ is included in SOLWEIG. Direct radiation perpendicular
to the solar beam should be used.

Environmental parameters
^^^^^^^^^^^^^^^^^^^^^^^^

Four main environmental parameters are mandatory; albedo and emissivity
of ground and walls. For building walls, these are bulk albedo values
with a default of 0.20 (albedo) and 0.90 (emissivity). If the ground
cover scheme is not used the bulk ground values are 0.15 (albedo) and
0.95 (emissivity).

If the ground cover scheme is activated (specific tick box found in the
plugin-interface), the variables for albedo, emissivity and how surface
temperature is parameterised for different surfaces is found in
**landcoverclasses\_v2016a.txt**. For as detailed description of the
ground cover scheme, see Lindberg et al. (2016)  [5]_.
**landcoverclasses\_v2016a.txt** can be found in
*C:\\Users\\your\_username\\.qgis2\\python\\plugins\\UMEP\\SOLWEIG*.

It should be noted that it is only grass and impervious surfaces that
has been parameterisised and evaluated. Other surfaces such as bare soil
and water are only first order approximations at this point.

Human exposure parameters
^^^^^^^^^^^^^^^^^^^^^^^^^

There are three human exposure parameters available:

-  *Absorption of shortwave radiation* (default value=0.70)
-  *Absorption of longwave radiation* (default value=0.95)
-  *Posture* (default value=Standing)

Optional settings
^^^^^^^^^^^^^^^^^

-  The original model as described in Lindberg et al. (2008)  [6]_ used
   an adjustment of sky emissivity (Jonsson et al. (2006)  [7]_
   calculated using the method presented in Prata (1996)  [8]_. This is
   now removed but can be added as an option.

-  As from version 2015a it is possible to consider the human as a
   cyliner instead of a box. See Holmer et al. (2015)  [9]_ for more
   details.

Output data
~~~~~~~~~~~

There are two forms of output available, calculated grids of various
parameters and full model outputs from certain point of interests (POIs)
within the model domain.

Surface grids
^^^^^^^^^^^^^

There are six different grids that can be saved from each model
iteration:

#. Mean radiation temperature
#. Incoming shortwave radiation
#. Outgoing shortwave radiation
#. Incoming longwave radiation
#. Outgoing longwave radiation
#. Shadow patterns

A post-processing plugin (SOLWEIG Analyzer) for the output grids are
planned to be included in future versions of UMEP.

POI.txt
^^^^^^^

By ticking in the option to include POIs (Point of Interest), a vector
point layer can be added and full model output are written out to text
files for the specific POI. Multiple POIs can be used by including many
points in the vector file. In the table below is the output variables
specifiedː

.. list-table::
   :widths: 5 20 75
   :header-rows: 1

   * - Column
     - Name
     - Description
   * - 1
     - iy
     - Year [YYYY]
   * - 2
     - id
     - Day of year [DOY]
   * - 3
     - it
     - Hour [H]
   * - 4
     - imin
     - Minute [M]
   * - 5
     - dectime
     - Decimal time [-]
   * - 6
     - altitude
     - altitude of the Sun [°]
   * - 7
     - azimuth
     - azimuth of the Sun [°]
   * - 8
     - kdir
     - direct beam solar radiation (from meteorological data) [W m\ :sup:`-2`]
   * - 9
     - kdiff
     - diffuse component of radiation (from meteorological data) [W m\ :sup:`-2`]
   * - 10
     - kglobal
     - global radiation (from meteorological data) [W m\ :sup:`-2`]
   * - 11
     - kdown
     - Incoming shortwave radiation [W m\ :sup:`-2`]
   * - 12
     - kup
     - Outgoing shortwave radiation [W m\ :sup:`-2`]
   * - 13
     - keast
     - Incoming shortwave radiation [W m\ :sup:`-2`]
   * - 14
     - ksouth
     - Outgoing shortwave radiation [W m\ :sup:`-2`]
   * - 15
     - kwest
     - Incoming shortwave radiation [W m\ :sup:`-2`]
   * - 16
     - knorth
     - Outgoing shortwave radiation [W m\ :sup:`-2`]
   * - 17
     - ldown
     - Incoming longwave radiation [W m\ :sup:`-2`]
   * - 18
     - lup
     - Outgoing longwave radiation [W m\ :sup:`-2`]
   * - 19
     - least
     - Incoming longwave radiation [W m\ :sup:`-2`]
   * - 20
     - lsouth
     - Outgoing longwave radiation [W m\ :sup:`-2`]
   * - 21
     - lwest
     - Incoming longwave radiation [W m\ :sup:`-2`]
   * - 22
     - lnorth
     - Outgoing longwave radiation [W m\ :sup:`-2`]
   * - 23
     - Ta
     - air temperature from meteorological data [°C]
   * - 24
     - Tg
     - calculated surface temperature [°C]
   * - 25
     - RH
     - relative humidity from meteorological data [percent]
   * - 26
     - Esky
     - sky emissivity
   * - 27
     - Tmrt
     - mean radiant temperature [°C]
   * - 28
     - I0
     - theoretical value of maximum incoming solar radiation [W m\ :sup:`-2`]
   * - 29
     - CI
     - clearness index
   * - 30
     - Shadow
     - Shadow value
   * - 31
     - SVF\_b
     - Sky View Factor from ground and buildings
   * - 32
     - SVF\_b+v
     - Sky View Factor from ground, buildings and vegetation
   * - 33
     - KsideI
     - Direct shortwave radiation from side if cylinder option is used


How to run the model
~~~~~~~~~~~~~~~~~~~~

The following section provides information on how to run the model and
what consideration that should be taken into account in order for the
model to perform at its best.

Run the model for example data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before running the model for your own data it is good to make certain
that you can run the test data and get the same results as in the
example files provided. Test/example files are given for Göteborg,
Sweden or London, UK. Here, you will use the Göteborg data.

#. Download and extract the test dataset to your computer
   (`testdata\_UMEP.zip <https://urban-meteorology-reading.github.io/>`__).
#. Add the raster layers (DSM, CDSM and land cover) from the Goteborg
   folder into a new QGIS session. The coordinate system of the grids is
   Sweref99 1200 (EPSG:3007).
#. In order to run SOLWEIG, some additional datasets must be created
   based on the raster grids you just added. Open the **SkyViewFactor
   Calculator** from the UMEP Pre-processor and calculate SVFs using
   both your DSM and CDSM. Leave all settings as default. This
   calculation produces a file called **svf.zip**' which is used later
   in the calculations.
#. Open the **Wall height and aspect** plugin from the UMEP
   Pre-processor and calculate both wall height and aspect using the DSM
   and your input raster. Make sure to add the result to your project.
#. Now you are ready to generate your first T\ :sub:`mrt` map. Open
   SOLWEIG and use the settings as shown below but replacing the paths
   to fit your computer environment. When you are finished, press Run.

.. figure:: /images/SOLWEIG_v2019a.png
   :width: 100%
   :alt:  none|Dialog for the SOLWEIG model

   Dialog for the SOLWEIG model

Tips and Tricks
~~~~~~~~~~~~~~~

-  All grids must have the same extent and pixel resolution.
-  The coordinate system of all the grids must be the same and translatable to lat, lon coordinates.
-  Meteorological file must have the default UMEP format.
-  Wall height and aspect grids as well as SVFs can be calculated from Pre-processor in UMEP. 
-  The model is very sensitive to the timing global radiation, i.e..
   that the peak of solar radiation occurs at local noon. If using a
   meteorological file included a longer dataset, this could be checked
   by comparing the global solar radiation and the theoretical maximum
   of solar radiation (I0) from a solar exposed point of interest.
-  Land cover grid should be in UMEP format.
-  A boolean building grid (building = 0, ground = 1) must be present, This grid is created either from a land cover or a ground DEM in conjunction with the building and ground DSM.
-  If using the land cover grid to derive the building grid, it is
   important that it coincides with the ground and building DSM.
   Otherwise strange results will be produced.
-  SOLWEIG focus on pedestrian radiation fluxes and it is not
   recommended to consider fluxes on building roofs.

Acknowledgements
~~~~~~~~~~~~~~~~

-  People who have contributed to the development of SOLWEIG (plus
   co-authors of papers):
-  Current contributors:

   -  Nils Wallenberg (Göteborg University, Sweden)
   -  C.S.B. Grimmond (University of Reading; previously Indiana
      University, King’s College London, UK),
   -  Fredrik Lindberg (Göteborg University, Sweden)
   -  Björn Holmer (Göteborg University, Sweden)

-  Past Contributors:

   -  Shiho Onomura (Göteborg University, Sweden)
   -  Sofia Thorsson (Göteborg University, Sweden)
   -  Ingegärd Eliasson (Göteborg University, Sweden)
   -  Janina Konarska (Göteborg University, Sweden)
   -  David Rayner (Göteborg University, Sweden)

-  Funding to support development:

   -  FORMAS, National Science Foundation (USA, BCS-0095284,
      ATM-0710631), EU Framework 7 BRIDGE (211345); EU emBRACE; UK Met
      Office; NERC ClearfLO, NERC TRUC.

Abbreviations
~~~~~~~~~~~~~

.. list-table::
   :widths: 10 50
   :header-rows: 1

   * - DEM
     - Digital Elevation Model
   * - DSM
     - Digital surface model
   * - DTM
     - Digital Terrain Model
   * - L↓
     - Incoming longwave radiation
   * - LAI
     - Leaf area index
   * - SOLWEIG
     - The solar and longwave environmental irradiance geometry model
   * - SVF
     - Sky view factor
   * - UMEP
     - `index_page`
   * - GUI
     - Graphical User Interface
   * - POI
     - Point of Interest

Development
~~~~~~~~~~~

SOLWEIG is an an open source model that we are keen to get others inputs
and contributions. There are two main ways to contribute:

#. Submit comments or issues to the
   `issue tracker <https://urban-meteorology-reading.github.io/>`__
#. Participate in Coding or adding new
   features `DevelopmentGuidelines`.


Version History
~~~~~~~~~~~~~~~

.. list-table::
   :widths: 15 85
   :header-rows: 1

   * - Version
     - Changes from previous version
   * - v2019a 
     - Possibilities to make use of an anisotrophic diffuse shortwave scheme is added. 
   * - v2018a
     - Minor bug fixing in ground view factor calculation. Introduction to PET and UTCI calculations for POIs. Available only for QGIS3.
   * - v2016a
     - First version released within UMEP. Python version of model is now released as open source.
   * - v2015a
     - -  Now includes a simple land cover scheme according to Lindberg et al. (2015)   * -
       -  Option to consider man as cylinder included (Holmer et al. 2015)   * -
       -  More options regarding incoming longwave radiation is added to the GUI
   * - v2014a
     - -  The model is now able to run at any time interval   * -
       -  A new format of the input met. data is introduced   * -
       -  The time stamp is now ‘fixed’ i.e., 1400 in an hourly dataset represent the hour before.
   * - 2013a
     - A new GUI is introduced as well as options to load gridded vegetation DSMs.
   * - 2.3
     - A new scheme for reflection concerning the shortwave fluxes is included taking into account sunlit and shaded walls
   * - 2.2
     - Some major (and minor) bugs have been fixed such as:   * -
       -  A major bug regarding the scale of trees and bushes is resolved
   * - 2.0
     - A new vegetation scheme is now included (Lindberg and Grimmond 2011). The interface also has a wizard for generating vegetation data to be included in the calculations. The new vegetation scheme is again slowing down the calculation but the computation time is still acceptable.
   * - 1.1
     - Longwave and shortwave radiation fluxes from the four cardinal points is now separated based on anisotropical Sky View Factor (SVF) images. Ground View Factors is introduced which is a parameter that is estimated based on what an instrument measuring Lup actually is seeing based on its height above ground and shadow patterns. In order to make accurate estimations of GVF, locations of building walls need to be known. Walls can be found automatically be the SOLWEIG-model. However, if the User wants to have more control over what are buildings and not, the User should use the marking tool included in the ‘Create/Edit Vegetation DEM’. A very simple approach taken from Offerle et al. (2003) is used to estimate nocturnal Ldown. Therefore Tmrt could also be estimated during night in version 1.1.
   * - 1.0
     - First version as from Lindberg et al. (2008)


References
~~~~~~~~~~

.. [1]
   Höppe P (1992) A new procedure to determine the mean radiant
   temperature outdoors. Wetter Leben 44:147–151.

.. [2]
   Lindberg F, Grimmond CSB, 2011: The influence of vegetation and
   building morphology on shadow patterns and mean radiant temperature
   in urban areas: model development and evaluation. Theoretical and
   Applied Climatology. 105(3), s. 311-323.

.. [3]
   Lindberg, F., Onomura, S. and Grimmond, C.S.B (2016) Influence of
   ground surface characteristics on the mean radiant temperature in
   urban areas. International Journal of Biometeorology. 60(9),
   1439-1452.

.. [4]
   Reindl D T, Beckman WA, Duffie JA, 1990: “Diffuse fraction
   correlation.” Solar energy 45(1): 1-7.

.. [5]

.. [6]
   Lindberg F, Thorsson S, Holmer B, 2008: SOLWEIG 1.0 – Modelling
   spatial variations of 3D radiant fluxes and mean radiant temperature
   in complex urban settings. International Journal of Biometeorology
   (2008) 52:697–713.

.. [7]
   Jonsson P, Eliasson I, Holmer B, Grimmond CSB (2006) Longwave
   incoming radiation in the Tropics: results from field work in three
   African cities. Theor Appl Climatol 85:185–201

.. [8]
   Prata AJ (1996) A new long-wave formula for estimating downward
   clearsky radiation at the surface. Q J R Meteorol Soc 122:1127–1151

.. [9]
   Holmer B, Lindberg F, Thorsson S, Rayner D, 2015: How to transform
   the standing man from a box to a cylinder – a modified methodology to
   calculate mean radiant temperature in field studies and models. ICUC9
   - 9th International Conference on Urban Climate jointly with 12th
   Symposium on the Urban Environment.
