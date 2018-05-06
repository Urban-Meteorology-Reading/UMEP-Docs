.. _Introduction:


Introduction
============

The Urban Multi-scale Environmental Predictor (**UMEP**) is a climate
services tool, designed for researchers, architects, urban planners,
climatologists, and meteorologists. This tool can be used for a variety
of applications related to outdoor thermal comfort, urban energy
consumption, climate change mitigation etc. **UMEP** consists of a
coupled modelling system which combines “state of the art” 1D and 2D
models related to the processes essential for urban climate
interactions.


**UMEP** is a `community <http://urban-climate.net/umep/People>`__ open
source model that users can contribute to improve and extend the
modelling capabilities. It is free to download. A major feature is the
ability for a user to interact with spatial information to determine
model parameters. The spatial data across a range of scales and sources
are accessed through **QGIS** - a cross-platform, free, open source
desktop geographic information systems
(`GIS <http://urban-climate.net/umep/Abbreviations>`__) application –
that provides data viewing, editing, and analysis capabilities.


UMEP: How to Cite
-----------------

Please use the reference below when UMEP is used:

``Lindberg F, Grimmond CSB, Gabey A, Huang B, Kent CW, Sun T, Theeuwes N, Järvi L, Ward H, Capel-Timms I, Chang YY, Jonsson P, Krave N, Liu D, Meyer D, Olofson F, Tan JG, Wästberg D, Xue L, Zhang Z (``\ **``2017``**\ ``) Urban Multi-scale Environmental Predictor (UMEP) - An integrated tool for city-based climate services.  Environmental Modelling and Software ``\ ````https://doi.org/10.1016/j.envsoft.2017.09.020`` <https://doi.org/10.1016/j.envsoft.2017.09.020>`__ <https://doi.org/10.1016/j.envsoft.2017.09.020>`__

The manual should be cited as:

``Lindberg F, Grimmond CSB, A Gabey, L Jarvi, CW Kent, N Krave, T Sun, N Wallenberg, HC Ward (``\ **``2017``**\ ``) Urban Multi-scale Environmental Predictor (UMEP) Manual. ``\ ```http://urban-climate.net/umep/UMEP_Manual`` <http://urban-climate.net/umep/UMEP_Manual>`__\ `` University of Reading UK, University of Gothenburg Sweden, SIMS China``


Current Version
---------------

This software is in continuous development. There are two types of
releases:

#. **Long term release** - (1.1) This can be obtained from the Plugin
   Manager in QGIS.
#. **Current development version** - (1.1.1) This can be obtained from
   the code `repository <http://bitbucket.org/fredrik_ucg/umep>`__. This
   version you need to install yourself.

Detailed information on how to install can be found
`here <http://urban-climate.net/umep/UMEP_Manual#Getting_Started>`__.

Information on version history can be found
`here <https://bitbucket.org/fredrik_ucg/umep/commits/all>`__.

Tool Architecture
-----------------

The UMEP plugin consist of three different parts; a pre-processor, a
processor and a post-processor. The pre-processor is used to prepare
spatial and meteorological data as inputs to the modelling system. The
processor includes all the main models for the main calculations. To
provide initial “quick looks” the post-processor will be enable results
to be plotted, statistics calculated etc. based on the model output.

**IMPORTANT!** It is strongly recommended to transform all geodatasets
into the same projected coordinate system (CRS) before any processing
starts.

+-----------------+-----------------+
| **UMEP**        | Description/\ * |
|                 | Applications*   |
+-----------------+-----------------+-----------------+-----------------+
| **Pre-Processor | Meteorological  | `Prepare        | Transforms      |
| **              | Data            | Existing        | meteorological  |
|                 |                 | Data <http://ur | data into UMEP  |
|                 |                 | ban-climate.net | format          |
|                 |                 | /umep/UMEP_Manu |                 |
|                 |                 | al#Meteorologic |                 |
|                 |                 | al_Data:_MetPre |                 |
|                 |                 | processor>`__   |                 |
+-----------------+-----------------+-----------------+-----------------+
| `Download data  | Prepare         |
| (WATCH) <http:/ | meteorological  |
| /www.urban-clim | dataset from    |
| ate.net/umep/UM | `WATCH <http:// |
| EP_Manual#Meteo | www.eu-watch.or |
| rological_Data: | g/data_availabi |
| _Download_data_ | lity>`__        |
| .28WATCH.29>`__ |                 |
+-----------------+-----------------+-----------------+-----------------+
| Spatial Data    | `Spatial Data   | Plugin for      |
|                 | Downloader <htt | retrieving      |
|                 | p://www.urban-c | geodata from    |
|                 | limate.net/umep | online services |
|                 | /UMEP_Manual#Sp | suitable for    |
|                 | atial_Data:_Spa | various UMEP    |
|                 | tial_Data_Downl | related tools   |
|                 | oader>`__       |                 |
+-----------------+-----------------+-----------------+-----------------+
| `DSM            | Creation/manipu |
| generator <http | lation          |
| ://www.urban-cl | of a DSM based  |
| imate.net/umep/ | on              |
| UMEP_Manual#Spa | user-specified  |
| tial_Data:_DSM_ | building        |
| Generator>`__   | footprint       |
|                 | vector data     |
|                 | and/or `Open    |
|                 | Street          |
|                 | Map <http://www |
|                 | .openstreetmap. |
|                 | org>`__         |
|                 | data (if        |
|                 | available)      |
+-----------------+-----------------+-----------------+-----------------+
| `Tree           | Creation/manipu |
| generator <http | lation          |
| ://www.urban-cl | of vegetation   |
| imate.net/umep/ | input data      |
| UMEP_Manual#Spa |                 |
| tial_Data:_Tree |                 |
| _Generator>`__  |                 |
+-----------------+-----------------+-----------------+-----------------+
| `LCZ            | Conversion from |
| Converter <http | Local Climate   |
| ://www.urban-cl | Zones (LCZs) in |
| imate.net/umep/ | the WUDAPT      |
| UMEP_Manual#Spa | database into   |
| tial_Data:_LCZ_ | SUEWS input     |
| Converter>`__   | data            |
+-----------------+-----------------+-----------------+-----------------+
| Urban geometry  | `Sky View       | Calculation of  |
|                 | Factor <http:// | continuous maps |
|                 | urban-climate.n | of Sky View     |
|                 | et/umep/UMEP_Ma | Factors (SVF)   |
|                 | nual#Urban_Geom | based on high   |
|                 | etry:_Sky_View_ | resolution      |
|                 | Factor_Calculat | digital surface |
|                 | or>`__          | models (DSM).   |
|                 |                 | *Solar access,  |
|                 |                 | urban heat      |
|                 |                 | island*         |
+-----------------+-----------------+-----------------+-----------------+
| `Wall Height    | Calculation of  |
| and             | height and      |
| Aspect <http:// | aspect of       |
| urban-climate.n | building walls  |
| et/umep/UMEP_Ma | based on a DSM  |
| nual#Urban_Geom |                 |
| etry:_Wall_Heig |                 |
| ht_and_Aspect>` |                 |
| __              |                 |
+-----------------+-----------------+-----------------+-----------------+
| Urban land      | `Land Cover     | Reclassifies a  |
| cover           | Reclassifier <h | grid into UMEP  |
|                 | ttp://urban-cli | format land     |
|                 | mate.net/umep/U | cover grid.     |
|                 | MEP_Manual#Urba | *Land surface   |
|                 | n_Land_Cover:_L | models*         |
|                 | and_Cover_Recla |                 |
|                 | ssifier>`__     |                 |
+-----------------+-----------------+-----------------+-----------------+
| `Land Cover     | Land cover      |
| Fraction        | fractions       |
| (Point) <http:/ | estimates from  |
| /urban-climate. | a land cover    |
| net/umep/UMEP_M | grid based on a |
| anual#Urban_Lan | specific point  |
| d_Cover:_Land_C | in space        |
| over_Reclassifi |                 |
| er>`__          |                 |
+-----------------+-----------------+-----------------+-----------------+
| `Land Cover     | Land cover      |
| Fraction        | fractions       |
| (Grid) <http:// | estimates from  |
| urban-climate.n | a land cover    |
| et/umep/UMEP_Ma | grid based on a |
| nual#Urban_Land | polygon grid    |
| _Cover:_Land_Co |                 |
| ver_Fraction_.2 |                 |
| 8Grid.29>`__    |                 |
+-----------------+-----------------+-----------------+-----------------+
| Urban           | `Morphometric   | Morphometric    |
| Morphology      | Calculator      | parameters from |
|                 | (Point) <http:/ | a DSM based on  |
|                 | /urban-climate. | a specific      |
|                 | net/umep/UMEP_M | point in space  |
|                 | anual#Urban_Mor |                 |
|                 | phology:_Morpho |                 |
|                 | metric_Calculat |                 |
|                 | or_.28Point.29> |                 |
|                 | `__             |                 |
+-----------------+-----------------+-----------------+-----------------+
| `Morphometric   | Morphometric    |
| Calculator      | parameters      |
| (Grid) <http:// | estimated from  |
| urban-climate.n | a DSM based on  |
| et/umep/UMEP_Ma | a polygon grid  |
| nual#Urban_Morp |                 |
| hology:_Morphom |                 |
| etric_Calculato |                 |
| r_.28Grid.29>`_ |                 |
| _               |                 |
+-----------------+-----------------+-----------------+-----------------+
| `Source Area    | Source area     |
| Model           | calculated from |
| (Point) <http:/ | a DSM based on  |
| /urban-climate. | a specific      |
| net/umep/UMEP_M | point in space. |
| anual#Urban_Mor | *Interpretation |
| phology:_Source | of              |
| _Area_.28Point. | observations*   |
| 29>`__          |                 |
+-----------------+-----------------+-----------------+-----------------+
| `SUEWS          | Preprocessing   |
| Prepare <http:/ | and preparing   |
| /urban-climate. | input data for  |
| net/umep/UMEP_M | the SUEWS model |
| anual#Pre-Proce |                 |
| ssor:_SUEWS_Pre |                 |
| pare>`__        |                 |
+-----------------+-----------------+-----------------+-----------------+
| **Processor**   | Outdoor Thermal | Comfort Index   | Spatial         |
|                 | Comfort         | (PET/UTCI)      | variations of   |
|                 |                 |                 | thermal comfort |
|                 |                 |                 | indices in      |
|                 |                 |                 | complex urban   |
|                 |                 |                 | environments    |
+-----------------+-----------------+-----------------+-----------------+
| `Mean Radiant   | Spatial         |
| Temperature     | variations of   |
| (SOLWEIG) <http | T\ :sub:`mrt`   |
| ://urban-climat | in complex      |
| e.net/umep/UMEP | urban           |
| _Manual#Outdoor | environments.   |
| _Thermal_Comfor | *Human Health:  |
| t:_SOLWEIG>`__  | Outdoor thermal |
|                 | comfort; Park   |
|                 | planning;       |
|                 | Heat/Health     |
|                 | warning; Daily  |
|                 | Operations:     |
|                 | visitors to     |
|                 | parks*          |
+-----------------+-----------------+-----------------+-----------------+
| Pedestrian Wind | Spatial         |
| Speed           | variations of   |
|                 | pedestrian wind |
|                 | speed in        |
|                 | complex urban   |
|                 | environments    |
+-----------------+-----------------+-----------------+-----------------+
| `ExtremeFinder  | Identify heat   |
| <http://www.urb | waves and cold  |
| an-climate.net/ | waves for a     |
| umep/UMEP_Manua | certain         |
| l#Outdoor_Therm | location.       |
| al_Comfort:_Ext | *Human Health:  |
| remeFinder>`__  | Outdoor thermal |
|                 | comfort; Daily  |
|                 | City            |
|                 | Operations:     |
|                 | Energy use; Gas |
|                 | consumption*    |
+-----------------+-----------------+-----------------+-----------------+
| Urban Energy    | Anthropogenic   | Spatial         |
| Balance         | Heat            | variations      |
|                 | (Q:sub:`F`)     | anthropogenic   |
|                 | (LQF)           | heat release    |
|                 |                 | for urban areas |
+-----------------+-----------------+-----------------+-----------------+
| `GQF <http://ww | Anthropogenic   |
| w.urban-climate | Heat            |
| .net/umep/UMEP_ | (Q:sub:`F`).    |
| Manual#Urban_En | *Daily City     |
| ergy_Balance:_G | Operations:     |
| QF>`__          | Energy use; Gas |
|                 | consumption;    |
|                 | Traffic heat    |
|                 | loads*          |
+-----------------+-----------------+-----------------+-----------------+
| `SUEWS          | Urban Energy    |
| (Simple) <http: | and Water       |
| //urban-climate | Balance.        |
| .net/umep/UMEP_ | *Disaster Risk  |
| Manual#Urban_En | Management:     |
| ergy_Balance:_U | Drought, Heat;  |
| rban_Energy_Bal | Environment     |
| ance_.28SUEWS.2 | evaluation for  |
| C_simple.29>`__ | construction,   |
|                 | Water           |
|                 | Management,     |
|                 | Green           |
|                 | infrastructure* |
+-----------------+-----------------+-----------------+-----------------+
| `SUEWS          | Urban Energy    |
| (Advanced) <htt | and Water       |
| p://urban-clima | Balance.        |
| te.net/umep/UME | *Disaster Risk  |
| P_Manual#Urban_ | Management:     |
| Energy_Balance: | Drought, Heat;  |
| _Urban_Energy_B | Environment     |
| alance_.28SUEWS | evaluation for  |
| .2FBLUEWS.2C_ad | construction,   |
| vanced.29>`__   | Water           |
|                 | Management,     |
|                 | Green           |
|                 | infrastructure* |
+-----------------+-----------------+-----------------+-----------------+
| Solar Radiation | `Solar Energy   | Solar           |
|                 | on Building     | irradiance on   |
|                 | Envelopes       | building roofs  |
|                 | (SEBE) <http:// | and walls in    |
|                 | www.urban-clima | urban           |
|                 | te.net/umep/UME | environments.   |
|                 | P_Manual#Solar_ | *Economy and    |
|                 | Radiation:_Sola | planning:       |
|                 | r_Energy_on_Bui | Energy          |
|                 | lding_Envelopes | production,     |
|                 | _.28SEBE.29>`__ | resource        |
|                 |                 | planning*       |
+-----------------+-----------------+-----------------+-----------------+
| `Daily Shadow   | Shadow patterns |
| Patterns <http: | on a DSM and    |
| //www.urban-cli | CDSM. *Economy  |
| mate.net/umep/U | and planning:   |
| MEP_Manual#Sola | Resource        |
| r_Radiation:_Da | planning Human  |
| ily_Shadow_Patt | Health: Outdoor |
| ern>`__         | thermal         |
|                 | comfort; Park   |
|                 | planning*       |
+-----------------+-----------------+-----------------+-----------------+
| **Post-Processo | Solar Radiation | `SEBE           | Visualisation   |
| r**             |                 | Visualisation < | of solar        |
|                 |                 | http://www.urba | irradiation on  |
|                 |                 | n-climate.net/u | building roofs  |
|                 |                 | mep/UMEP_Manual | and walls based |
|                 |                 | #Solar_Radiatio | on SEBE model   |
|                 |                 | n:_SEBE_.28Visu | results         |
|                 |                 | alisation.29>`_ |                 |
|                 |                 | _               |                 |
+-----------------+-----------------+-----------------+-----------------+
| Outdoor Thermal | `SOLWEIG        | Plugin for      |
| Comfort         | analyzer <http: | plotting,       |
|                 | //www.urban-cli | statistical     |
|                 | mate.net/umep/U | analysis and    |
|                 | MEP_Manual#Outd | post-processing |
|                 | oor_Thermal_Com | of model        |
|                 | fort:_SOLWEIG_A | results from    |
|                 | nalyzer>`__     | SOLWEIG         |
+-----------------+-----------------+-----------------+-----------------+
| Urban Energy    | `SUEWS          | Plugin for      |
| Balance         | analyser <http: | plotting and    |
|                 | //urban-climate | statistical     |
|                 | .net/umep/UMEP_ | analysis of     |
|                 | Manual#Urban_En | model results   |
|                 | ergy_Balance:_S | from SUEWS      |
|                 | UEWS_Analyser>` | simple and      |
|                 | __              | SUEWS advanced  |
+-----------------+-----------------+-----------------+-----------------+
| Benchmark       | `Benchmark      | For statistical |
|                 | System <http:// | analysis of     |
|                 | urban-climate.n | model results,  |
|                 | et/umep/UMEP_Ma | such as SUEWS   |
|                 | nual#Benchmark_ |                 |
|                 | System>`__      |                 |
+-----------------+-----------------+-----------------+-----------------+

+---------+
| Planned |
+---------+
|  |
+---------+

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

.. figure:: SUEWSworkflow.png
   :alt: centre| Workflow and geodata used for analysing urban energy balance using the SUEWS model. Bold outlined boxes are mandatory items. Yellow, orange and red indicates pre-processor, processor and post-processor tools, respectively. Grey boxes indicate geodatasets.

   centre\| Workflow and geodata used for analysing urban energy balance
   using the SUEWS model. Bold outlined boxes are mandatory items.
   Yellow, orange and red indicates pre-processor, processor and
   post-processor tools, respectively. Grey boxes indicate geodatasets.

.. figure:: SOLWEIGworkflow.png
   :alt: centre| Workflow and geodata used for analysing mean radiant temperature using the SOLWEIG model. Bold outlines are mandatory items. Yellow, orange and red indicates pre-processor, processor and post-processor tools, respectively. Grey boxes indicate geodatasets.

   centre\| Workflow and geodata used for analysing mean radiant
   temperature using the SOLWEIG model. Bold outlines are mandatory
   items. Yellow, orange and red indicates pre-processor, processor and
   post-processor tools, respectively. Grey boxes indicate geodatasets.

Other application examples can be found
`here <http://www.urban-climate.net/umep/Example_Applications>`__.

Evaluation and application studies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+-----------------------+-----------------------+-----------------------+
| Name                  | References:           | References:           |
|                       | Evaluation            | Application           |
+=======================+=======================+=======================+
| Mean Radiant          | +--------+--------+   | +--------+--------+   |
| Temperature           | | Spatia | Refere |   | | Spatia | Refere |   |
| (`SOLWEIG <http://urb | | l      | nce    |   | | l      | nce    |   |
| an-climate.net/umep/S | | refere |        |   | | refere |        |   |
| OLWEIG>`__)           | | nce    |        |   | | nce    |        |   |
|                       | +========+========+   | +========+========+   |
|                       | | Gothen | `Lindb |   | | London | `Lindb |   |
|                       | | burg,  | erg    |   | | ,      | erg    |   |
|                       | | Sweden | et al. |   | | UK     | and    |   |
|                       | |        | (2008) |   | |        | Grimmo |   |
|                       | |        |  <http |   | |        | nd     |   |
|                       | |        | ://lin |   | |        | (2011) |   |
|                       | |        | k.spri |   | |        |  <http |   |
|                       | |        | nger.c |   | |        | ://lin |   |
|                       | |        | om/art |   | |        | k.spri |   |
|                       | |        | icle/1 |   | |        | nger.c |   |
|                       | |        | 0.1007 |   | |        | om/art |   |
|                       | |        | /s0048 |   | |        | icle/1 |   |
|                       | |        | 4-008- |   | |        | 0.1007 |   |
|                       | |        | 0162-7 |   | |        | /s1125 |   |
|                       | |        | >`__   |   | |        | 2-011- |   |
|                       | +--------+--------+   | |        | 0184-5 |   |
|                       | | Gothen | `Lindb |   | |        | >`__   |   |
|                       | | burg,  | erg    |   | +--------+--------+   |
|                       | | Sweden | and    |   | | Gothen | `Lindb |   |
|                       | |        | Grimmo |   | | burg,  | erg    |   |
|                       | |        | nd     |   | | Sweden | et al. |   |
|                       | |        | (2011) |   | |        | (2013) |   |
|                       | |        |  <http |   | |        |  <http |   |
|                       | |        | ://lin |   | |        | ://lin |   |
|                       | |        | k.spri |   | |        | k.spri |   |
|                       | |        | nger.c |   | |        | nger.c |   |
|                       | |        | om/art |   | |        | om/art |   |
|                       | |        | icle/1 |   | |        | icle/1 |   |
|                       | |        | 0.1007 |   | |        | 0.1007 |   |
|                       | |        | /s0070 |   | |        | /s0048 |   |
|                       | |        | 4-010- |   | |        | 4-013- |   |
|                       | |        | 0382-8 |   | |        | 0638-y |   |
|                       | |        | >`__   |   | |        | >`__   |   |
|                       | +--------+--------+   | +--------+--------+   |
|                       | | Freibu | `Lindb |   | | Stockh | `Lindb |   |
|                       | | rg,    | erg    |   | | olm,   | erg    |   |
|                       | | German | and    |   | | Sweden | et al. |   |
|                       | | y      | Grimmo |   | |        | (2013) |   |
|                       | |        | nd     |   | |        |  <http |   |
|                       | |        | (2011) |   | |        | ://lin |   |
|                       | |        |  <http |   | |        | k.spri |   |
|                       | |        | ://lin |   | |        | nger.c |   |
|                       | |        | k.spri |   | |        | om/art |   |
|                       | |        | nger.c |   | |        | icle/1 |   |
|                       | |        | om/art |   | |        | 0.1007 |   |
|                       | |        | icle/1 |   | |        | /s0048 |   |
|                       | |        | 0.1007 |   | |        | 4-013- |   |
|                       | |        | /s0070 |   | |        | 0638-y |   |
|                       | |        | 4-010- |   | |        | >`__   |   |
|                       | |        | 0382-8 |   | +--------+--------+   |
|                       | |        | >`__   |   | | Luleå, | `Lindb |   |
|                       | +--------+--------+   | | Sweden | erg    |   |
|                       | | Kassel | `Lindb |   | |        | et al. |   |
|                       | | ,      | erg    |   | |        | (2013) |   |
|                       | | German | and    |   | |        |  <http |   |
|                       | | y      | Grimmo |   | |        | ://lin |   |
|                       | |        | nd     |   | |        | k.spri |   |
|                       | |        | (2011) |   | |        | nger.c |   |
|                       | |        |  <http |   | |        | om/art |   |
|                       | |        | ://lin |   | |        | icle/1 |   |
|                       | |        | k.spri |   | |        | 0.1007 |   |
|                       | |        | nger.c |   | |        | /s0048 |   |
|                       | |        | om/art |   | |        | 4-013- |   |
|                       | |        | icle/1 |   | |        | 0638-y |   |
|                       | |        | 0.1007 |   | |        | >`__   |   |
|                       | |        | /s0070 |   | +--------+--------+   |
|                       | |        | 4-010- |   | | Adelai | `Thom  |   |
|                       | |        | 0382-8 |   | | de,    | et al. |   |
|                       | |        | >`__   |   | | Austra | (2016) |   |
|                       | +--------+--------+   | | lia    |  <http |   |
|                       | | London | `Lindb |   | |        | ://www |   |
|                       | | ,      | erg    |   | |        | .scien |   |
|                       | | UK     | et al. |   | |        | cedire |   |
|                       | |        | (2016) |   | |        | ct.com |   |
|                       | |        |  <http |   | |        | /scien |   |
|                       | |        | ://lin |   | |        | ce/art |   |
|                       | |        | k.spri |   | |        | icle/p |   |
|                       | |        | nger.c |   | |        | ii/S16 |   |
|                       | |        | om/art |   | |        | 188667 |   |
|                       | |        | icle/1 |   | |        | 163012 |   |
|                       | |        | 0.1007 |   | |        | 97>`__ |   |
|                       | |        | /s0048 |   | +--------+--------+   |
|                       | |        | 4-016- |   | | Berlin | `Jänic |   |
|                       | |        | 1135-x |   | | ,      | ke     |   |
|                       | |        | >`__   |   | | German | et al. |   |
|                       | +--------+--------+   | | y      | (2015) |   |
|                       | | Hong   | `Lau   |   | |        |  <http |   |
|                       | | Kong,  | et al. |   | |        | ://www |   |
|                       | | China  | (2016) |   | |        | .scien |   |
|                       | |        |  <http |   | |        | cedire |   |
|                       | |        | ://www |   | |        | ct.com |   |
|                       | |        | .scien |   | |        | /scien |   |
|                       | |        | cedire |   | |        | ce/art |   |
|                       | |        | ct.com |   | |        | icle/p |   |
|                       | |        | /scien |   | |        | ii/S22 |   |
|                       | |        | ce/art |   | |        | 120955 |   |
|                       | |        | icle/p |   | |        | 153003 |   |
|                       | |        | ii/S03 |   | |        | 41>`__ |   |
|                       | |        | 787788 |   | +--------+--------+   |
|                       | |        | 153006 |   | | Gothen | `Lau   |   |
|                       | |        | 45>`__ |   | | burg,  | et al. |   |
|                       | +--------+--------+   | | Sweden | (2014) |   |
|                       | | Shangh | `Chen  |   | |        |  <http |   |
|                       | | ai,    | et al. |   | |        | ://lin |   |
|                       | | China  | (2016) |   | |        | k.spri |   |
|                       | |        |  <http |   | |        | nger.c |   |
|                       | |        | ://www |   | |        | om/art |   |
|                       | |        | .scien |   | |        | icle/1 |   |
|                       | |        | cedire |   | |        | 0.1007 |   |
|                       | |        | ct.com |   | |        | /s0048 |   |
|                       | |        | /scien |   | |        | 4-014- |   |
|                       | |        | ce/art |   | |        | 0898-1 |   |
|                       | |        | icle/p |   | |        | >`__   |   |
|                       | |        | ii/S03 |   | +--------+--------+   |
|                       | |        | 787788 |   | | Frankf | `Lau   |   |
|                       | |        | 163081 |   | | urt,   | et al. |   |
|                       | |        | 2X>`__ |   | | German | (2014) |   |
|                       | +--------+--------+   | | y      |  <http |   |
|                       |                       | |        | ://lin |   |
|                       |                       | |        | k.spri |   |
|                       |                       | |        | nger.c |   |
|                       |                       | |        | om/art |   |
|                       |                       | |        | icle/1 |   |
|                       |                       | |        | 0.1007 |   |
|                       |                       | |        | /s0048 |   |
|                       |                       | |        | 4-014- |   |
|                       |                       | |        | 0898-1 |   |
|                       |                       | |        | >`__   |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Porto, | `Lau   |   |
|                       |                       | | Portug | et al. |   |
|                       |                       | | al     | (2014) |   |
|                       |                       | |        |  <http |   |
|                       |                       | |        | ://lin |   |
|                       |                       | |        | k.spri |   |
|                       |                       | |        | nger.c |   |
|                       |                       | |        | om/art |   |
|                       |                       | |        | icle/1 |   |
|                       |                       | |        | 0.1007 |   |
|                       |                       | |        | /s0048 |   |
|                       |                       | |        | 4-014- |   |
|                       |                       | |        | 0898-1 |   |
|                       |                       | |        | >`__   |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Gothen | `Lindb |   |
|                       |                       | | burg,  | erg    |   |
|                       |                       | | Sweden | et al. |   |
|                       |                       | |        | (2016) |   |
|                       |                       | |        |  <http |   |
|                       |                       | |        | ://www |   |
|                       |                       | |        | .scien |   |
|                       |                       | |        | cedire |   |
|                       |                       | |        | ct.com |   |
|                       |                       | |        | /scien |   |
|                       |                       | |        | ce/art |   |
|                       |                       | |        | icle/p |   |
|                       |                       | |        | ii/S22 |   |
|                       |                       | |        | 106707 |   |
|                       |                       | |        | 163005 |   |
|                       |                       | |        | 79>`__ |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Gothen | `Thors |   |
|                       |                       | | burg,  | son    |   |
|                       |                       | | Sweden | et al. |   |
|                       |                       | |        | (2011) |   |
|                       |                       | |        |  <http |   |
|                       |                       | |        | ://onl |   |
|                       |                       | |        | inelib |   |
|                       |                       | |        | rary.w |   |
|                       |                       | |        | iley.c |   |
|                       |                       | |        | om/doi |   |
|                       |                       | |        | /10.10 |   |
|                       |                       | |        | 02/joc |   |
|                       |                       | |        | .2231/ |   |
|                       |                       | |        | abstra |   |
|                       |                       | |        | ct>`__ |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Stockh | `Thors |   |
|                       |                       | | olm,   | son    |   |
|                       |                       | | Sweden | et al. |   |
|                       |                       | |        | (2014) |   |
|                       |                       | |        |  <http |   |
|                       |                       | |        | ://www |   |
|                       |                       | |        | .scien |   |
|                       |                       | |        | cedire |   |
|                       |                       | |        | ct.com |   |
|                       |                       | |        | /scien |   |
|                       |                       | |        | ce/art |   |
|                       |                       | |        | icle/p |   |
|                       |                       | |        | ii/S22 |   |
|                       |                       | |        | 120955 |   |
|                       |                       | |        | 140000 |   |
|                       |                       | |        | 54>`__ |   |
|                       |                       | +--------+--------+   |
+-----------------------+-----------------------+-----------------------+
| Pedestrian Wind Speed | +--------+--------+   |                       |
|                       | | Spatia | Refere |   |                       |
|                       | | l      | nce    |   |                       |
|                       | | refere |        |   |                       |
|                       | | nce    |        |   |                       |
|                       | +========+========+   |                       |
|                       | | Global | `Johan |   |                       |
|                       | |        | sson   |   |                       |
|                       | |        | et al. |   |                       |
|                       | |        | (2015) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://lin |   |                       |
|                       | |        | k.spri |   |                       |
|                       | |        | nger.c |   |                       |
|                       | |        | om/art |   |                       |
|                       | |        | icle/1 |   |                       |
|                       | |        | 0.1007 |   |                       |
|                       | |        | /s0070 |   |                       |
|                       | |        | 4-015- |   |                       |
|                       | |        | 1405-2 |   |                       |
|                       | |        | >`__   |   |                       |
|                       | +--------+--------+   |                       |
+-----------------------+-----------------------+-----------------------+
| Anthropogenic Heat    | +--------+--------+   | +--------+--------+   |
| (Qf) (LUCY)           | | Spatia | Refere |   | | Spatia | Refere |   |
|                       | | l      | nce    |   | | l      | nce    |   |
|                       | | refere |        |   | | refere |        |   |
|                       | | nce    |        |   | | nce    |        |   |
|                       | +========+========+   | +========+========+   |
|                       | | Global | `Allen |   | | Europe | `Lindb |   |
|                       | |        | et al. |   | |        | erg    |   |
|                       | |        | (2011) |   | |        | et al. |   |
|                       | |        |  <http |   | |        | (2013) |   |
|                       | |        | ://onl |   | |        |  <http |   |
|                       | |        | inelib |   | |        | ://www |   |
|                       | |        | rary.w |   | |        | .scien |   |
|                       | |        | iley.c |   | |        | cedire |   |
|                       | |        | om/doi |   | |        | ct.com |   |
|                       | |        | /10.10 |   | |        | /scien |   |
|                       | |        | 02/joc |   | |        | ce/art |   |
|                       | |        | .2210/ |   | |        | icle/p |   |
|                       | |        | abstra |   | |        | ii/S22 |   |
|                       | |        | ct>`__ |   | |        | 120955 |   |
|                       | +--------+--------+   | |        | 130000 |   |
|                       |                       | |        | 59>`__ |   |
|                       |                       | +--------+--------+   |
+-----------------------+-----------------------+-----------------------+
| Urban Energy and      | +--------+--------+   | +--------+--------+   |
| Water Balance         | | Spatia | Refere |   | | Spatia | Refere |   |
| (`SUEWS <http://urban | | l      | nce    |   | | l      | nce    |   |
| -climate.net/umep/SUE | | refere |        |   | | refere |        |   |
| WS>`__)               | | nce    |        |   | | nce    |        |   |
|                       | +========+========+   | +========+========+   |
|                       | | Vancou | `Järvi |   | | London | Ward   |   |
|                       | | ver,   | et al. |   | | ,      | and    |   |
|                       | | Canada | (2011) |   | | UK     | Grimmo |   |
|                       | |        |  <http |   | |        | nd     |   |
|                       | |        | ://www |   | |        | (2017) |   |
|                       | |        | .scien |   | +--------+--------+   |
|                       | |        | cedire |   | | Helsin | `Nordb |   |
|                       | |        | ct.com |   | | ki,    | o      |   |
|                       | |        | /scien |   | | Finlan | et al. |   |
|                       | |        | ce/art |   | | d      | (2015) |   |
|                       | |        | icle/p |   | |        |  <http |   |
|                       | |        | ii/S00 |   | |        | ://www |   |
|                       | |        | 221694 |   | |        | .scien |   |
|                       | |        | 110069 |   | |        | cedire |   |
|                       | |        | 37>`__ |   | |        | ct.com |   |
|                       | +--------+--------+   | |        | /scien |   |
|                       | | Los    | `Järvi |   | |        | ce/art |   |
|                       | | Angele | et al. |   | |        | icle/p |   |
|                       | | s,     | (2011) |   | |        | ii/S22 |   |
|                       | | USA    |  <http |   | |        | 120955 |   |
|                       | |        | ://www |   | |        | 150001 |   |
|                       | |        | .scien |   | |        | 9X>`__ |   |
|                       | |        | cedire |   | +--------+--------+   |
|                       | |        | ct.com |   | | Dublin | `Alexa |   |
|                       | |        | /scien |   | | ,      | nder   |   |
|                       | |        | ce/art |   | | Irelan | et al. |   |
|                       | |        | icle/p |   | | d      | (2016) |   |
|                       | |        | ii/S00 |   | |        |  <http |   |
|                       | |        | 221694 |   | |        | ://www |   |
|                       | |        | 110069 |   | |        | .scien |   |
|                       | |        | 37>`__ |   | |        | cedire |   |
|                       | +--------+--------+   | |        | ct.com |   |
|                       | | Helsin | `Järvi |   | |        | /scien |   |
|                       | | ki,    | et al. |   | |        | ce/art |   |
|                       | | Finlan | (2014) |   | |        | icle/p |   |
|                       | | d      |  <http |   | |        | ii/S01 |   |
|                       | |        | ://www |   | |        | 692046 |   |
|                       | |        | .geosc |   | |        | 160001 |   |
|                       | |        | i-mode |   | |        | 28>`__ |   |
|                       | |        | l-dev. |   | +--------+--------+   |
|                       | |        | net/7/ |   | | Porto, | `Rafae |   |
|                       | |        | 1691/2 |   | | Portug | l      |   |
|                       | |        | 014/>` |   | | al     | et al. |   |
|                       | |        | __     |   | |        | (2016) |   |
|                       | +--------+--------+   | |        |  <http |   |
|                       | | Montre | `Järvi |   | |        | ://www |   |
|                       | | al,    | et al. |   | |        | .scien |   |
|                       | | Canada | (2014) |   | |        | cedire |   |
|                       | |        |  <http |   | |        | ct.com |   |
|                       | |        | ://www |   | |        | /scien |   |
|                       | |        | .geosc |   | |        | ce/art |   |
|                       | |        | i-mode |   | |        | icle/p |   |
|                       | |        | l-dev. |   | |        | ii/S00 |   |
|                       | |        | net/7/ |   | |        | 489697 |   |
|                       | |        | 1691/2 |   | |        | 163120 |   |
|                       | |        | 014/>` |   | |        | 86>`__ |   |
|                       | |        | __     |   | +--------+--------+   |
|                       | +--------+--------+   |                       |
|                       | | Dublin | `Alexa |   |                       |
|                       | | ,      | nder   |   |                       |
|                       | | Irelan | et al. |   |                       |
|                       | | d      | (2015) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://dx. |   |                       |
|                       | |        | doi.or |   |                       |
|                       | |        | g/10.1 |   |                       |
|                       | |        | 016/j. |   |                       |
|                       | |        | uclim. |   |                       |
|                       | |        | 2015.0 |   |                       |
|                       | |        | 5.001> |   |                       |
|                       | |        | `__    |   |                       |
|                       | +--------+--------+   |                       |
|                       | | Swindo | `Ward  |   |                       |
|                       | | n,     | et al. |   |                       |
|                       | | UK     | (2016) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://www |   |                       |
|                       | |        | .scien |   |                       |
|                       | |        | cedire |   |                       |
|                       | |        | ct.com |   |                       |
|                       | |        | /scien |   |                       |
|                       | |        | ce/art |   |                       |
|                       | |        | icle/p |   |                       |
|                       | |        | ii/S22 |   |                       |
|                       | |        | 120955 |   |                       |
|                       | |        | 163002 |   |                       |
|                       | |        | 56>`__ |   |                       |
|                       | +--------+--------+   |                       |
|                       | | London | `Ward  |   |                       |
|                       | | ,      | et al. |   |                       |
|                       | | UK     | (2016) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://www |   |                       |
|                       | |        | .scien |   |                       |
|                       | |        | cedire |   |                       |
|                       | |        | ct.com |   |                       |
|                       | |        | /scien |   |                       |
|                       | |        | ce/art |   |                       |
|                       | |        | icle/p |   |                       |
|                       | |        | ii/S22 |   |                       |
|                       | |        | 120955 |   |                       |
|                       | |        | 163002 |   |                       |
|                       | |        | 56>`__ |   |                       |
|                       | +--------+--------+   |                       |
|                       | | Helsin | `Karsi |   |                       |
|                       | | ki,    | sto    |   |                       |
|                       | | Finlam | et al. |   |                       |
|                       | | d      | (2016) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://onl |   |                       |
|                       | |        | inelib |   |                       |
|                       | |        | rary.w |   |                       |
|                       | |        | iley.c |   |                       |
|                       | |        | om/doi |   |                       |
|                       | |        | /10.10 |   |                       |
|                       | |        | 02/qj. |   |                       |
|                       | |        | 2659/f |   |                       |
|                       | |        | ull>`_ |   |                       |
|                       | |        | _      |   |                       |
|                       | +--------+--------+   |                       |
|                       | | Shangh | (Radia |   |                       |
|                       | | ai,    | tion)  |   |                       |
|                       | | China  | `Ao et |   |                       |
|                       | |        | al.    |   |                       |
|                       | |        | (2016) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://jou |   |                       |
|                       | |        | rnals. |   |                       |
|                       | |        | ametso |   |                       |
|                       | |        | c.org/ |   |                       |
|                       | |        | doi/ab |   |                       |
|                       | |        | s/10.1 |   |                       |
|                       | |        | 175/JA |   |                       |
|                       | |        | MC-D-1 |   |                       |
|                       | |        | 6-0082 |   |                       |
|                       | |        | .1>`__ |   |                       |
|                       | +--------+--------+   |                       |
|                       | | Sacram | `Onomu |   |                       |
|                       | | ento,  | ra     |   |                       |
|                       | | US     | et al. |   |                       |
|                       | |        | (2015) |   |                       |
|                       | |        |  <http |   |                       |
|                       | |        | ://www |   |                       |
|                       | |        | .scien |   |                       |
|                       | |        | cedire |   |                       |
|                       | |        | ct.com |   |                       |
|                       | |        | /scien |   |                       |
|                       | |        | ce/art |   |                       |
|                       | |        | icle/p |   |                       |
|                       | |        | ii/S22 |   |                       |
|                       | |        | 120955 |   |                       |
|                       | |        | 140008 |   |                       |
|                       | |        | 56>`__ |   |                       |
|                       | +--------+--------+   |                       |
+-----------------------+-----------------------+-----------------------+
| Solar Energy on       | +--------+--------+   | +--------+--------+   |
| Building Envelopes    | | Spatia | Refere |   | | Spatia | Refere |   |
| (SEBE)                | | l      | nce    |   | | l      | nce    |   |
|                       | | refere |        |   | | refere |        |   |
|                       | | nce    |        |   | | nce    |        |   |
|                       | +========+========+   | +========+========+   |
|                       | | Gothen | `Lindb |   | | Dar es | `Lau   |   |
|                       | | burg,  | erg    |   | | Salam, | et al. |   |
|                       | | Sweden | et al. |   | | Tanzan | (2016) |   |
|                       | |        | (2015) |   | | ia     |  <http |   |
|                       | |        |  <http |   | |        | ://www |   |
|                       | |        | ://www |   | |        | .scien |   |
|                       | |        | .scien |   | |        | cedire |   |
|                       | |        | cedire |   | |        | ct.com |   |
|                       | |        | ct.com |   | |        | /scien |   |
|                       | |        | /scien |   | |        | ce/art |   |
|                       | |        | ce/art |   | |        | icle/p |   |
|                       | |        | icle/p |   | |        | ii/S22 |   |
|                       | |        | ii/S00 |   | |        | 106707 |   |
|                       | |        | 38092X |   | |        | 163042 |   |
|                       | |        | 150011 |   | |        | 67>`__ |   |
|                       | |        | 64>`__ |   | +--------+--------+   |
|                       | +--------+--------+   | | Stockh | `Onlin |   |
|                       |                       | | olm,   | e      |   |
|                       |                       | | Sweden | mappin |   |
|                       |                       | |        | g      |   |
|                       |                       | |        | servic |   |
|                       |                       | |        | e      |   |
|                       |                       | |        | (in    |   |
|                       |                       | |        | Swedis |   |
|                       |                       | |        | h) <ht |   |
|                       |                       | |        | tp://w |   |
|                       |                       | |        | ww.ene |   |
|                       |                       | |        | rgirad |   |
|                       |                       | |        | givnin |   |
|                       |                       | |        | gen.se |   |
|                       |                       | |        | /sites |   |
|                       |                       | |        | /all/t |   |
|                       |                       | |        | hemes/ |   |
|                       |                       | |        | energi |   |
|                       |                       | |        | /map/i |   |
|                       |                       | |        | ndex.h |   |
|                       |                       | |        | tml>`_ |   |
|                       |                       | |        | _      |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Uppsal | `Onlin |   |
|                       |                       | | a,     | e      |   |
|                       |                       | | Sweden | mappin |   |
|                       |                       | |        | g      |   |
|                       |                       | |        | servic |   |
|                       |                       | |        | e      |   |
|                       |                       | |        | (in    |   |
|                       |                       | |        | Swedis |   |
|                       |                       | |        | h) <ht |   |
|                       |                       | |        | tp://e |   |
|                       |                       | |        | c2-54- |   |
|                       |                       | |        | 77-203 |   |
|                       |                       | |        | -12.eu |   |
|                       |                       | |        | -west- |   |
|                       |                       | |        | 1.comp |   |
|                       |                       | |        | ute.am |   |
|                       |                       | |        | azonaw |   |
|                       |                       | |        | s.com/ |   |
|                       |                       | |        | uppsal |   |
|                       |                       | |        | a/>`__ |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Gothen | `Onlin |   |
|                       |                       | | burg,  | e      |   |
|                       |                       | | Sweden | mappin |   |
|                       |                       | |        | g      |   |
|                       |                       | |        | servic |   |
|                       |                       | |        | e      |   |
|                       |                       | |        | (in    |   |
|                       |                       | |        | Swedis |   |
|                       |                       | |        | h) <ht |   |
|                       |                       | |        | tp://w |   |
|                       |                       | |        | ww.got |   |
|                       |                       | |        | eborge |   |
|                       |                       | |        | nergi. |   |
|                       |                       | |        | se/Pri |   |
|                       |                       | |        | vat/Pr |   |
|                       |                       | |        | ojekt_ |   |
|                       |                       | |        | och_et |   |
|                       |                       | |        | ableri |   |
|                       |                       | |        | ngar/F |   |
|                       |                       | |        | ornyba |   |
|                       |                       | |        | r_ener |   |
|                       |                       | |        | gi/Sol |   |
|                       |                       | |        | celler |   |
|                       |                       | |        | /Solka |   |
|                       |                       | |        | rtan/> |   |
|                       |                       | |        | `__    |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Eskils | `Onlin |   |
|                       |                       | | tuna,  | e      |   |
|                       |                       | | Sweden | mappin |   |
|                       |                       | |        | g      |   |
|                       |                       | |        | servic |   |
|                       |                       | |        | e      |   |
|                       |                       | |        | (in    |   |
|                       |                       | |        | Swedis |   |
|                       |                       | |        | h) <ht |   |
|                       |                       | |        | tp://k |   |
|                       |                       | |        | arta.e |   |
|                       |                       | |        | skilst |   |
|                       |                       | |        | una.se |   |
|                       |                       | |        | /eskil |   |
|                       |                       | |        | stunak |   |
|                       |                       | |        | artan/ |   |
|                       |                       | |        | x/#map |   |
|                       |                       | |        | s/1069 |   |
|                       |                       | |        | >`__   |   |
|                       |                       | +--------+--------+   |
+-----------------------+-----------------------+-----------------------+
| Daily Shadow Patterns | +--------+--------+   | +--------+--------+   |
|                       | | Spatia | Refere |   | | Spatia | Refere |   |
|                       | | l      | nce    |   | | l      | nce    |   |
|                       | | refere |        |   | | refere |        |   |
|                       | | nce    |        |   | | nce    |        |   |
|                       | +========+========+   | +========+========+   |
|                       | | Borås, | `Hu et |   | | London | `Lindb |   |
|                       | | Sweden | al.    |   | | ,      | erg    |   |
|                       | |        | (2015) |   | | UK     | et al. |   |
|                       | |        |  <http |   | |        | (2015) |   |
|                       | |        | ://lin |   | |        |  <http |   |
|                       | |        | k.spri |   | |        | ://www |   |
|                       | |        | nger.c |   | |        | .scien |   |
|                       | |        | om/art |   | |        | cedire |   |
|                       | |        | icle/1 |   | |        | ct.com |   |
|                       | |        | 0.1007 |   | |        | /scien |   |
|                       | |        | /s0070 |   | |        | ce/art |   |
|                       | |        | 4-015- |   | |        | icle/p |   |
|                       | |        | 1508-9 |   | |        | ii/S22 |   |
|                       | |        | >`__   |   | |        | 120955 |   |
|                       | +--------+--------+   | |        | 140009 |   |
|                       |                       | |        | 0X>`__ |   |
|                       |                       | +--------+--------+   |
|                       |                       | | Gothen | `Lindb |   |
|                       |                       | | burg,  | erg    |   |
|                       |                       | | Sweden | et al. |   |
|                       |                       | |        | (2011) |   |
|                       |                       | |        |  <http |   |
|                       |                       | |        | ://www |   |
|                       |                       | |        | .scien |   |
|                       |                       | |        | cedire |   |
|                       |                       | |        | ct.com |   |
|                       |                       | |        | /scien |   |
|                       |                       | |        | ce/art |   |
|                       |                       | |        | icle/p |   |
|                       |                       | |        | ii/S02 |   |
|                       |                       | |        | 66352X |   |
|                       |                       | |        | 110006 |   |
|                       |                       | |        | 93>`__ |   |
|                       |                       | +--------+--------+   |
+-----------------------+-----------------------+-----------------------+
|  |
+-----------------------+-----------------------+-----------------------+

.. |Source area modelling with UMEP| image:: Header_umep.png
