.. _Introduction to SUEWS:

Introduction To Suews
^^^^^^^^^^^^^^^^^^^^^^^^

Introduction
------------

In this tutorial you will use a land-surface model,
`SUEWS <http://urban-climate.net/umep/SUEWS>`__ to simulate energy
exchanges in a city (London is the test case).

SUEWS (Surface Urban Energy and Water Balance Scheme) allows the energy and water balance exchanges for urban areas to be modelled (Järvi et al. 2011, 2014, Ward et al. 2016a). The model is applicable at the neighbourhood scale (e.g. 10\ :sup:`2` to 10\ :sup:`4` m). The fluxes calculated are applicable to height of about 2-3 times the mean height of the roughness elements; i.e. above the `roughness sublayer (RSL) <http://glossary.ametsoc.org/wiki/Roughness_sublayer>`__. The use of SUEWS within Urban Multi-scale Environmental Predictor (UMEP) provides an introduction to the model and the processes simulated, the parameters used and the impact on the resulting fluxes.

Tools such as this, once appropriately assessed for an area, can be used for a broad range of applications. For example, for climate services (e.g. http://www.wmo.int/gfcs/). Running a model can allow analyses, assessments, and long-term projections and scenarios. Most applications require not only meteorological data but also information about the activities that occur in the area of interest (e.g. agriculture, population, road and infrastructure, and socio-economic variables).                                                                                    |

 Model output may be needed in many formats depending on a users’ needs. Thus, the format must be useful, while ensuring the science included within the model is appropriate. Figure 1 provides an overview of `UMEP <http://urban-climate.net/umep/UMEP>`__, a city based climate service tool (CBCST). Within UMEP there are a number of models which can predict and diagnose a range of meteorological processes. In this activity we are concerned with SUEWS, initially the central components of the model. See `manual <http://urban-climate.net/umep/SUEWS>`__ or published **papers** for more detailed information of the model.

        .. figure:: /images/UMEP_overview.png
        Figure 1: Overview of the climate service tool UMEP (Grimmond et al. 2015)

SUEWS can be run in a number of different ways:

#. Within UMEP via the Simple selection. This is useful for becoming
   familiar with the model (Part 1)
#. Within UMEP via the Advanced selection. This can be used to exploit
   the full capabilities of the model (Part 2)
#. SUEWS standalone (see
   `manual <http://urban-climate.net/umep/SUEWS>`__)
#. Within other larger scale models (e.g. WRF).

SUEWS Simple Objectives
-----------------------

To introduce SUEWS and how to run the model within `UMEP (Urban
Multi-scale Environmental
Predictor) <http://urban-climate.net/umep/UMEP_Manual>`__. `Help with
Abbreviations <http://urban-climate.net/umep/UMEP_Manual#Abbreviations>`__

Steps
~~~~~

#. An introduction to the model and how it is designed.
#. Different kinds of input data that are needed to run the model
#. How to run the model
#. How to examine the model output

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

SUEWS Model Inputs
------------------

Details of the model inputs and outputs are provided in the `SUEWS
manual <http://urban-climate.net/umep/SUEWS>`__. As this tutorial is
concerned with a **simple application** only the most critical
parameters are shown. Other versions allow many other parameters to be
modified to more appropriate values if applicable. The table below
provides an overview of the parameters that can be modified in the
Simple application of SUEWS.

.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - Type
     - Definition
     - Reference/Comments
   * -
     - **Building/ Tree Morphology**
     -
   * - Mean height of Building/Trees (m)
     -
     - `Grimmond and Oke (1999), Fig 2 <http://journals.ametsoc.org/doi/10.1175/1520-0450%281999%29038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
   * - Frontal area index (m:sup:`2`/ m\ :sup:`2`)
     - Area of the front face of a roughness element exposed to the wind relative to the plan area.
     - `Grimmond and Oke (1999), Fig 2 <http://journals.ametsoc.org/doi/10.1175/1520-0450%281999%29038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
   * - Plan area index (m:sup:`2`/ m\ :sup:`2`)
     - Area of the roughness elements relative to the total plan area.
     - `Grimmond and Oke (1999), Fig 2 <http://journals.ametsoc.org/doi/10.1175/1520-0450%281999%29038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__. Should be the same value as the land cover fractions for buildings and sum for trees, respectively.
   * -
     - **Land cover fraction**
     - Should sum to 1
   * - Paved
     - Roads, sidewalks, parking lots, impervious surfaces that are not buildings
     -
   * - Buildings
     - Buildings
     - Same as the plan area index of buildings in the morphology section.
   * - Evergreen trees
     - Trees/shrubs that retain their leaves/needles all year round
     - Tree plan area index will be the sum of evergreen and deciduous area. Note: this is the same as the plan area index of vegetation in the morphology section.
   * - Deciduous trees
     - Trees/shrubs that lose their leaves
     - Same as above
   * - Grass
     - Grass
     -
   * - Bare soil
     - Bare soil – non vegetated but water can infilitrate
     -
   * - Water
     - River, ponds, swimming pools, fountains
     -
   * -
     - **Initial conditions**
     - What is the state of the conditions when the model run begins?
   * - Days since rain (days)
     - This will influence irrigation behaviour in the model. If there has been rain recently then it will be longer before irrigiation occurs.
     - If this is a period or location when no irrigation is permitted/occurring then this is not critical as the model will calculate from this point going forward.
   * - Daily mean temperature (°C)
     - Influences irrigation and anthropogenic heat flux
     -
   * - Soil mositure status (%)
     - This will influence both evaporation and runoff processes
     - If close to 100 % then there is plenty of water for evaporation but also a higher probability of flooding if intense precipitation occurs.
   * -
     - **Other**
     -
   * - Year
     - What days are weekdays/weekends
     -
   * - Latitude (°)
     - Solar related calculations
     -
   * - Longitude (°)
     - Solar related calculations
     -
   * - `UTC (h) <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`__
     - Time zone
     - Influences solar related calculations

How to Run SuewsSimple from the UMEP-plugin
-------------------------------------------

#. Open SuewsSimple from *UMEP -> Processor -> Urban Energy Balance ->
   Urban Energy Balance, SUEWS (Simple)*. The GUI that opens looks quite
   extensive but it is actually not that complicated to start a basic
   model run (Figure 2). Some additional information about the plugin is
   found in the left window. As you can read, a **test dataset** from
   observations for London, UK (`Kotthaus and Grimmond
   2014 <http://www.sciencedirect.com/science/article/pii/S2212095513000503>`__,
   `Ward et al.
   2016a <http://www.sciencedirect.com/science/article/pii/S2212095516300256>`__)
   is included in within the plugin.

        .. figure:: /images/Simple2.png

#. To make use of this dataset click on **Add settings from test
   dataset** (see near bottom of the box). The land cover fractions and
   all other settings originate from Kotthaus and Grimmond (2014). They
   used a source area model to obtain the different input parameters
   (their `Fig. 7 in Kotthaus and Grimmond,
   2014 <http://www.sciencedirect.com/science/article/pii/S2212095513000497>`__).
#. Before you start the model, change the location of the output data to
   any location of your choice. Also, make notes on the settings such as
   *Year* etc.
#. Do a model run and explore the results by clicking **Run**. A command
   window appears, when SUEWS performs the calculations using the
   settings from the interface. Once the calculations are done, some of
   the results are shown in two summary plots.

          .. figure:: /images/1350px-SuewsSimplefig1.png

          .. figure:: /images/1350px-SuewsSimplefig2.png

Model results
-------------

The graphs in Figure 3a are the monthly mean energy (left) and water
balance (right). The lower graphs (Figure 3b) show the radiation fluxes,
energy fluxes, and water related outputs throughout the year. This plot
includes a lot of data and it might be difficult to examine it in
detail.

To zoom into the plot: use the tools in the top left corner, to zoom to
a period of interest. For example, the Zoom in to about the last ten
days in March (Figure 4). This was a period with clear relatively
weather.

        .. figure:: /images/SuewsSimplefig2zoom.png
          :alt:  900px|center|Figure 4: Zoom in on end of March from the daily plot in Figure 3b.



Saving a Figure
---------------

Use the disk tool in the upper left corner.

#. .jpg
#. .pdf
#. .tif (Recommended)
#. .png

Output data Files
-----------------

In the output folder (you selected earlier) you will find (at least)
three files:

#. **Kc98\_2012\_60.txt** – provides the 60 min model results for site
   “KC1” for the year 2012
#. **Kc\_FilesChoices.txt** – this indicates all options used in the
   model run see the SUEWS Manual for interpretation of content (this is
   for when you are doing large number of runs so you know exactly what
   options were used in each run)
#. **Kc98\_DailyState.txt** – this provides the daily mean state (see
   SUEWS manual for detailed explanation). This allows you to see, for
   example, the daily state of the LAI (leaf area index).
#. **Kc\_OutputFormat.txt** – provides detailed information about the
   output files such as extended descriptions for each column including
   units.

If you open these files in a text editor. To understand the header
variables read the `SUEWS
manual <http://urban-climate.net/umep/SUEWS#Output_files>`__.

Sensitivity to land surface fractions
-------------------------------------

    .. figure:: /images/450px-LCFs.png

The previous results are for a densely build-up area in
London, UK. In order to test the sensitivity of SUEWS to some surface
properties you can think about changing some of the surface properties
in the SUEWS Simple. For example, change the land cover fraction by:

#. Change the land cover fractions as seen in the figure. Feel free to
   select other values as long as all the fractions *add up to 1.0*.
#. Save the output to a different folder by selecting *output folder*.
#. Click *Run*.

`Advanced SUEWS Tutorial <../Tutorials/SUEWSAdvanced.html>`__
------------------------------------------------------------------------------------------------------------------

`Reporting a bug <http://urban-climate.net/umep/UMEP_Manual#How_to_Contribute>`__
---------------------------------------------------------------------------------

References
----------

-  Grimmond CSB and Oke 1999: Aerodynamic properties of urban areas
   derived, from analysis of surface form. `Journal of Applied
   Climatology 38:9,
   1262-1292 <http://journals.ametsoc.org/doi/abs/10.1175/1520-0450(1999)038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
-  Grimmond et al. 2015: Climate Science for Service Partnership: China,
   Shanghai Meteorological Servce, Shanghai, China, August 2015.
-  Järvi L, Grimmond CSB & Christen A 2011: The Surface Urban Energy and
   Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver
   `J. Hydrol. 411,
   219-237 <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
-  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB 2014:
   Development of the Surface Urban Energy and Water balance Scheme
   (SUEWS) for cold climate cities, , `Geosci. Model Dev. 7,
   1691-1711 <http://www.geosci-model-dev.net/7/1691/2014/>`__
-  Kormann R, Meixner FX 2001: An analytical footprint model for
   non-neutral stratification. `Bound.-Layer Meteorol., 99,
   207–224 <http://www.sciencedirect.com/science/article/pii/S2212095513000497#b0145>`__
-  Kotthaus S and Grimmond CSB 2014: Energy exchange in a dense urban
   environment – Part II: Impact of spatial heterogeneity of the
   surface. `Urban Climate 10,
   281–307 <http://www.sciencedirect.com/science/article/pii/S2212095513000497>`__
-  Onomura S, Grimmond CSB, Lindberg F, Holmer B, Thorsson S 2015:
   Meteorological forcing data for urban outdoor thermal comfort models
   from a coupled convective boundary layer and surface energy balance
   scheme. Urban Climate. 11:1-23 `(link to
   paper) <http://www.sciencedirect.com/science/article/pii/S2212095514000856>`__
-  Ward HC, L Järvi, S Onomura, F Lindberg, A Gabey, CSB Grimmond 2016
   SUEWS Manual V2016a, http://urban-climate.net/umep/SUEWS Department
   of Meteorology, University of Reading, Reading, UK
-  Ward HC, Kotthaus S, Järvi L and Grimmond CSB 2016b: Surface Urban
   Energy and Water Balance Scheme (SUEWS): Development and evaluation
   at two UK sites. `Urban Climate
   http://dx.doi.org/10.1016/j.uclim.2016.05.001 <http://www.sciencedirect.com/science/article/pii/S2212095516300256>`__
-  Ward HC, S Kotthaus, CSB Grimmond, A Bjorkegren, M Wilkinson, WTJ
   Morrison, JG Evans, JIL Morison, M Iamarino 2015b: Effects of urban
   density on carbon dioxide exchanges: observations of dense urban,
   suburban and woodland areas of southern England. `Env Pollution 198,
   186-200 <http://dx.doi.org/10.1016/j.envpol.2014.12.031>`__

Authors this document: Lindberg and Grimmond (2016)

Definitions and Notation
------------------------

To help you find further information about the acronyms they are
classified by **T**: Type of term: **C**: computer term, **S**: science
term, **G**: GIS term.

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * -
     - Definition
     - T
     - Reference/Comment
   * - DEM
     - Digital elevation model
     - G
     -
   * - DSM
     - Digital surface model
     - G
     -
   * - FAI (λ:sub:`F`)
     - Frontal area index
     - S
     - `Grimmond and Oke (1999) <http://journals.ametsoc.org/doi/abs/10.1175/1520-0450(1999)038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__, their figure 2
   * - GUI
     - Graphical User Interface
     - C
     -
   * - LAI
     - Leaf Area Index
     - S
     -
   * - PAI (λ:sub:`P`)
     - Plan area index
     - S
     -
   * - png
     - Portable Network Graphics
     - C
     - format for saving plots/figures
   * - QGIS
     -
     - G
     - `http://www.qgis.org/en/site/ <http://www.qgis.org/en/site/>`__
   * - SUEWS
     - Surface Urban Energy and Water Balance Scheme
     - S
     -
   * - Tif
     - Tagged Image File Format
     - C
     - format for saving plots/figures
   * - UI
     - user interface
     - C
     -
   * - UMEP
     - Urban Multi-scale Environmental predictor
     - C
     -
   * - z\ :sub:`0`
     - Roughness length for momentum
     - S
     - `Grimmond and Oke (1999) <http://journals.ametsoc.org/doi/abs/10.1175/1520-0450(1999)038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
   * - z\ :sub:`d`
     - Zero plane displacement length for momentum
     - S
     - `Grimmond and Oke (1999) <http://journals.ametsoc.org/doi/abs/10.1175/1520-0450(1999)038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__

Further explanation
-------------------

Morphometric Methods to determine Roughness parameters:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For more and overview and details see `Grimmond and Oke
(1999) <http://journals.ametsoc.org/doi/abs/10.1175/1520-0450%281999%29038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
and `Kent et al.
(2017a) <https://link.springer.com/article/10.1007%2Fs10546-017-0248-z>`__.
This uses the height and spacing of roughness elements (e.g. buildings,
trees) to model the roughness parameters. For more details see `Kent et
al.
(2017a) <https://link.springer.com/article/10.1007%2Fs10546-017-0248-z>`__,
`Kent et al.
(2017b) <http://www.sciencedirect.com/science/article/pii/S0167610516307346?via%3Dihub>`__
and [Kent et al. (2017c)]. UMEP has tools for doing this: *Pre-processor
-> Urban Morphology*

Source Area Model
~~~~~~~~~~~~~~~~~

For more details see `Kotthaus and Grimmond
(2014b) <http://www.sciencedirect.com/science/article/pii/S2212095513000497>`__
and `Kent et al.
(2017a) <https://link.springer.com/article/10.1007%2Fs10546-017-0248-z>`__.
The `Kormann and Meixner
(2001) <https://link.springer.com/article/10.1023%2FA%3A1018991015119>`__
model is used to determine the probable area that a turbulent flux
measurement was impacted by. This is a function of wind direction,
stability, turbulence characteristics (friction velocity, variance of
the lateral wind velocity) and roughness parameters.
