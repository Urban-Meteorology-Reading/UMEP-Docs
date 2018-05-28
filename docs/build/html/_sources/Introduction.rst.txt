.. _Introduction:


Introduction
============

The Urban Multi-scale Environmental Predictor (**UMEP**) is a climate
services tool, designed for researchers, architects, urban planners,
climatologists, and meteorologists. This tool can be used for a variety
of applications related to outdoor thermal comfort, urban energy
consumption, climate change mitigation etc. **UMEP** consists of a
coupled modelling system which combines “state of the art” 1D and 2D
models related to the processes essen tial for urban climate
interactions.

**UMEP** is a `community <People_Involved_&_Acknowledgements>` open
source model that users can contribute to improve and extend the
modelling capabilities. It is free to download. A major feature is the
ability for a user to interact with spatial information to determine
model parameters. The spatial data across a range of scales and sources
are accessed through **QGIS** - a cross-platform, free, open source
desktop geographic information systems
(`GIS <Abbreviations>`) application –
that provides data viewing, editing, and analysis capabilities.

This software is in continuous development. There are two types of
releases:

#. **Long term release** - this may be obtained from the QGIS plugin
   manager `(see details) <Getting_Started>`.
#. **Current development version** - this can be obtained from the plugin
   `repository <http://www.bitbucket.org/fredrik_ucg/umep>`__. This
   version you need to manually install yourself `(see details) <Getting_Started>`.

The UMEP plugin consist of three
parts; a pre-processor, a processor and a post-processor. The
pre-processor prepares spatial and meteorological data as inputs to the
modelling system. The processor includes all the main models for the
main calculations. To provide initial “quick looks” the post-processor
will enable results to be plotted, statistics calculated etc. based on
the model output. For more information on the content and archetecture,
see `PluginArchitecture`.


Detailed information on how to install can be found `here <Getting_Started>`.

Information on version history can be found `here <https://bitbucket.org/fredrik_ucg/umep/commits/branch/master>`__.


UMEP: How to Cite
-----------------

Please use the reference below when UMEP is used:

.. epigraph::

  *Lindberg F, Grimmond CSB, Gabey A, Huang B, Kent CW, Sun T, Theeuwes N, Järvi L, Ward H, Capel-
  Timms I, Chang YY, Jonsson P, Krave N, Liu D, Meyer D, Olofson F, Tan JG, Wästberg D, Xue L,
  Zhang Z (2017) Urban Multi-scale Environmental Predictor (UMEP) - An integrated tool for city-based 
  climate services. Environmental Modelling and Software. https://doi.org/10.1016/j.envsoft.2017.09.020*

  
The manual should be cited as:

.. epigraph::

  *Lindberg F, Grimmond CSB, A Gabey, L Jarvi, CW Kent, N Krave, T Sun, N Wallenberg, HC Ward (2018) 
  Urban Multi-scale Environmental Predictor (UMEP) Manual. http://urban-climate.net/umep/ UMEP_Manual.
  University of Reading UK, University of Gothenburg Sweden, SIMS China*


.. _PluginArchitecture:

Plugin Architecture
-------------------

The UMEP plugin consist of three different parts; a pre-processor, a
processor and a post-processor. The pre-processor is used to prepare
spatial and meteorological data as inputs to the modelling system. The
processor includes all the main models for the main calculations. To
provide initial “quick looks” the post-processor will be enable results
to be plotted, statistics calculated etc. based on the model output.

.. note:: It is strongly recommended to transform all geodatasets into the same projected coordinate system (CRS) before any processing starts.


Pre-Processor
~~~~~~~~~~~~~

**Meteorological Data**

.. list-table:: 
   :widths: 35 65
   :header-rows: 0

   * - `Prepare Existing Data <MetPreprocessor>`
     - Transforms meteorological data into UMEP format
   * - `Download data (WATCH) <WATCH>`
     - Prepare meteorological dataset from `WATCH <http://www.eu-watch.org/data_availability>`__

	 
**Spatial Data**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Spatial Data Downloader <SpatialDataDownloader>`
     - Plugin for retrieving geodata from online services suitable for various UMEP related tools
   * - `DSM generator <DSMGenerator>`
     - Creation/manipulation of a DSM based on user-specified building footprint vector data and/or `Open Street Map <http://www.openstreetmap.org>`__ data (if available)
   * - `Tree generator <TreeGenerator>`
     - Creation/manipulation of vegetation input data
   * - `LCZ Converter <LCZConverter>`
     - Conversion from Local Climate Zones (LCZs) in the WUDAPT database into SUEWS input data

**Urban geometry**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Sky View Factor <SkyViewFactorCalculator>`
     - Calculation of continuous maps of Sky View Factors (SVF) based on high resolution digital surface models (DSM). *Solar access, urban heat island*
   * - `Wall Height and Aspect <WallHeightandAspect>`
     - Calculation of height and aspect of building walls based on a DSM

**Urban land cover**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Land Cover Reclassifier <LandCoverReclassifier>`
     - Reclassifies a grid into UMEP format land cover grid. *Land surface models*
   * - `Land Cover Fraction (Point) <LandCoverFraction(Point)>`
     - Land cover fractions estimates from a land cover grid based on a specific point in space
   * - `Land Cover Fraction (Grid) <LandCoverFraction(Grid)>`
     - Land cover fractions estimates from a land cover grid based on a polygon grid

**Urban Morphology**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Morphometric Calculator (Point) <MorphometricCalculator(Point)>`
     - Morphometric parameters from a DSM based on a specific point in space
   * - `Morphometric Calculator (Grid) <MorphometricCalculator(Grid)>`__
     - Morphometric parameters estimated from a DSM based on a polygon grid
   * - `Source Area Model (Point) <SourceArea(Point)>`
     - Source area calculated from a DSM based on a specific point in space. *Interpretation of observations*

**Other**

.. list-table::
   :widths: 35 65
   :header-rows: 0
   
   * - `SUEWS Prepare <SUEWSPrepare>`
     - Preprocessing and preparing input data for the SUEWS model


Processor
~~~~~~~~~

**Outdoor Thermal Comfort**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - Comfort Index (PET/UTCI) (planned)
     - Spatial variations of thermal comfort indices in complex urban environments
   * - `Mean Radiant Temperature (SOLWEIG) <SOLWEIG>`
     - Spatial variations of T\ :sub:`mrt` in complex urban environments. *Human Health: Outdoor thermal comfort; Park planning; Heat/Health warning; Daily Operations: visitors to parks*
   * - Pedestrian Wind Speed (planned)
     - Spatial variations of pedestrian wind speed in complex urban environments
   * - `ExtremeFinder <ExtremeFinder>`
     - Identify heat waves and cold waves for a certain location. *Human Health: Outdoor thermal comfort; Daily City Operations: Energy use; Gas consumption*


**Urban Energy Balance**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `LQF <LQF>`
     - Spatial variations anthropogenic heat release for urban areas
   * - `GQF <GQF>`
     - Anthropogenic Heat (Q\ :sub:`F`). *Daily City Operations: Energy use; Gas consumption; Traffic heat loads*
   * - `SUEWS (Simple) <SUEWSSimple>`
     - Urban Energy and Water Balance. *Disaster Risk Management: Drought, Heat; Environment evaluation for construction, Water Management, Green infrastructure*
   * - `SUEWS (Advanced) <SUEWSadvanced>`
     - Urban Energy and Water Balance. *Disaster Risk Management: Drought, Heat; Environment evaluation for construction, Water Management, Green infrastructure*

 
**Solar Radiation**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Solar Energy on Building Envelopes (SEBE) <SEBE>`
     - Solar irradiance on building roofs and walls in urban environments. *Economy and planning: Energy production, resource planning*
   * - `Daily Shadow Patterns <DailyShadowPattern>`
     - Shadow patterns on a DSM and CDSM. *Economy and planning: Resource planning Human Health: Outdoor thermal comfort; Park planning*


Post-Processor
~~~~~~~~~~~~~~
**Solar Radiation**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `SEBE Visualisation <SEBEVisualisation>`
     - Plugin to visualse output irradiation from SEBE on building roofs, walls and ground 


**Outdoor Thermal Comfort**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `SOLWEIG analyzer <SOLWEIGAnalyzer>`
     - Plugin for plotting, statistical analysis and post-processing of model results from SOLWEIG

 
**Urban Energy Balance**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `SUEWS analyser <SUEWSAnalyser>`
     - Plugin for plotting and statistical analysis of model results from SUEWS simple and SUEWS advanced


**Benchmark**

.. list-table::
   :widths: 35 65
   :header-rows: 0

   * - `Benchmark System <Benchmark>`
     - For statistical analysis of model results, such as SUEWS


Tool Applications
-----------------

A key element of UMEP is to facilitate the preparation of input data
needed for City-Based Climate Services (CBCS). UMEP provides both
guidance and tools that enable data preparation and manipulation. This
is particularly important as many end-users have familiarity with some,
but not the full spectrum, of the data needed for applications. Below
you can find some examples on applications and workflows for the
modelling procedure in UMEP and what tools that are connected to each
other.

.. figure:: /images/SUEWSworkflow.png
   :alt:   Workflow and geodata used for analysing urban energy balance using the SUEWS model. Bold outlined boxes are mandatory items. Yellow, orange and red indicates pre-processor, processor and post-processor tools, respectively. Grey boxes indicate geodatasets.

   Workflow and geodata used for analysing urban energy balance
   using the SUEWS model. Bold outlined boxes are mandatory items.
   Yellow, orange and red indicates pre-processor, processor and
   post-processor tools, respectively. Grey boxes indicate geodatasets.

.. figure:: /images/SOLWEIGworkflow.png
   :alt:  Workflow and geodata used for analysing mean radiant temperature using the SOLWEIG model. Bold outlines are mandatory items. Yellow, orange and red indicates pre-processor, processor and post-processor tools, respectively. Grey boxes indicate geodatasets.

   Workflow and geodata used for analysing mean radiant
   temperature using the SOLWEIG model. Bold outlines are mandatory
   items. Yellow, orange and red indicates pre-processor, processor and
   post-processor tools, respectively. Grey boxes indicate geodatasets.

Other application examples can be found
`here <http://www.urban-climate.net/umep/Example_Applications>`__.

Evaluation and application studies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Mean Radiant Temperature (`SOLWEIG <http://urban-climate.net/umep/SOLWEIG>`__)
      - References: Evaluation
  
      .. list-table::
         :widths: 50 50
         :header-rows: 1

         * - Spatial reference
           - Reference
         * - Gothenburg, Sweden
           - `Lindberg et al. (2008) <http://link.springer.com/article/10.1007/s00484-008-0162-7>`__
         * - Gothenburg, Sweden
           - `Lindberg and Grimmond (2011) <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
         * - Freiburg, Germany
           - `Lindberg and Grimmond (2011) <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
         * - Kassel, Germany
           - `Lindberg and Grimmond (2011) <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
         * - London, UK
           - `Lindberg et al. (2016) <http://link.springer.com/article/10.1007/s00484-016-1135-x>`__
         * - Hong Kong, China
           - `Lau et al. (2016) <http://www.sciencedirect.com/science/article/pii/S0378778815300645>`__
         * - Shanghai, China
           - `Chen et al. (2016) <http://www.sciencedirect.com/science/article/pii/S037877881630812X>`__
      - References: Application
	  
      .. list-table::
         :widths: 50 50
         :header-rows: 1

         * - Spatial reference
           - Reference
         * - London, UK
           - `Lindberg and Grimmond (2011) <http://link.springer.com/article/10.1007/s11252-011-0184-5>`__
         * - Gothenburg, Sweden
           - `Lindberg et al. (2013) <http://link.springer.com/article/10.1007/s00484-013-0638-y>`__
         * - Stockholm, Sweden
           - `Lindberg et al. (2013) <http://link.springer.com/article/10.1007/s00484-013-0638-y>`__
         * - Luleå, Sweden
           - `Lindberg et al. (2013) <http://link.springer.com/article/10.1007/s00484-013-0638-y>`__
         * - Adelaide, Australia
           - `Thom et al. (2016) <http://www.sciencedirect.com/science/article/pii/S1618866716301297>`__
         * - Berlin, Germany
           - `Jänicke et al. (2015) <http://www.sciencedirect.com/science/article/pii/S2212095515300341>`__
         * - Gothenburg, Sweden
           - `Lau et al. (2014) <http://link.springer.com/article/10.1007/s00484-014-0898-1>`__
         * - Frankfurt, Germany
           - `Lau et al. (2014) <http://link.springer.com/article/10.1007/s00484-014-0898-1>`__
         * - Porto, Portugal
           - `Lau et al. (2014) <http://link.springer.com/article/10.1007/s00484-014-0898-1>`__
         * - Gothenburg, Sweden
           - `Lindberg et al. (2016) <http://www.sciencedirect.com/science/article/pii/S2210670716300579>`__
         * - Gothenburg, Sweden
           - `Thorsson et al. (2011) <http://onlinelibrary.wiley.com/doi/10.1002/joc.2231/abstract>`__
         * - Stockholm, Sweden
           - `Thorsson et al. (2014) <http://www.sciencedirect.com/science/article/pii/S2212095514000054>`__

* Pedestrian Wind Speed
            - References: Evaluation
            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Global
                 - `Johansson et al. (2015) <http://link.springer.com/article/10.1007/s00704-015-1405-2>`__


* Anthropogenic Heat (Qf) (LUCY)
            - References: Evaluation

            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Global
                 - `Allen et al. (2011) <http://onlinelibrary.wiley.com/doi/10.1002/joc.2210/abstract>`__
            - References: Application

            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Europe
                 - `Lindberg et al. (2013) <http://www.sciencedirect.com/science/article/pii/S2212095513000059>`__


* Urban Energy and Water Balance (`SUEWS <http://urban-climate.net/umep/SUEWS>`__)
            - References: Evaluation
			
            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Vancouver, Canada
                 - `Järvi et al. (2011) <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
               * - Los Angeles, USA
                 - `Järvi et al. (2011) <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
               * - Helsinki, Finland
                 - `Järvi et al. (2014) <http://www.geosci-model-dev.net/7/1691/2014/>`__
               * - Montreal, Canada
                 - `Järvi et al. (2014) <http://www.geosci-model-dev.net/7/1691/2014/>`__
               * - Dublin, Ireland
                 - `Alexander et al. (2015) <http://dx.doi.org/10.1016/j.uclim.2015.05.001>`__
               * - Swindon, UK
                 - `Ward et al. (2016) <http://www.sciencedirect.com/science/article/pii/S2212095516300256>`__
               * - London, UK
                 - `Ward et al. (2016) <http://www.sciencedirect.com/science/article/pii/S2212095516300256>`__
               * - Helsinki, Finlamd
                 - `Karsisto et al. (2016) <http://onlinelibrary.wiley.com/doi/10.1002/qj.2659/full>`__
               * - Shanghai, China
                 - (Radiation) `Ao et al. (2016) <http://journals.ametsoc.org/doi/abs/10.1175/JAMC-D-16-0082.1>`__
               * - Sacramento, US
                 - `Onomura et al. (2015) <http://www.sciencedirect.com/science/article/pii/S2212095514000856>`__

            - References: Application
			
            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - London, UK
                 - Ward and Grimmond (2017)
               * - Helsinki, Finland
                 - `Nordbo et al. (2015) <http://www.sciencedirect.com/science/article/pii/S221209551500019X>`__
               * - Dublin, Ireland
                 - `Alexander et al. (2016) <http://www.sciencedirect.com/science/article/pii/S0169204616000128>`__
               * - Porto, Portugal
                 - `Rafael et al. (2016) <http://www.sciencedirect.com/science/article/pii/S0048969716312086>`__


* Solar Energy on Building Envelopes (SEBE)
            - References: Evaluation

            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Gothenburg, Sweden
                 - `Lindberg et al. (2015) <http://www.sciencedirect.com/science/article/pii/S0038092X15001164>`__

            - References: Application

            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Dar es Salam, Tanzania
                 - `Lau et al. (2016) <http://www.sciencedirect.com/science/article/pii/S2210670716304267>`__
               * - Stockholm, Sweden
                 - `Online mapping service (in Swedish) <http://www.energiradgivningen.se/sites/all/themes/energi/map/index.html>`__
               * - Uppsala, Sweden
                 - `Online mapping service (in Swedish) <http://ec2-54-77-203-12.eu-west-1.compute.amazonaws.com/uppsala/>`__
               * - Gothenburg, Sweden
                 - `Online mapping service (in Swedish) <http://www.goteborgenergi.se/Privat/Projekt_och_etableringar/Fornybar_energi/Solceller/Solkartan/>`__
               * - Eskilstuna, Sweden
                 - `Online mapping service (in Swedish) <http://karta.eskilstuna.se/eskilstunakartan/x/#maps/1069>`__

* Daily Shadow Patterns
            - References: Evaluation

            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - Borås, Sweden
                 - `Hu et al. (2015) <http://link.springer.com/article/10.1007/s00704-015-1508-9>`__
            
            - References: Application
            .. list-table::
               :widths: 50 50
               :header-rows: 1

               * - Spatial reference
                 - Reference
               * - London, UK
                 - `Lindberg et al. (2015) <http://www.sciencedirect.com/science/article/pii/S221209551400090X>`__
               * - Gothenburg, Sweden
                 - `Lindberg et al. (2011) <http://www.sciencedirect.com/science/article/pii/S0266352X11000693>`__