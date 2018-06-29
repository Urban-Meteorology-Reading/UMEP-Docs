.. _tutorials_intro:


Tutorials
============

To help users getting started with UMEP, the community is working on
setting up tutorials and instructions for different parts of the UMEP
tool. The tutorials are available are found in the table below.

.. note:: One essential part when working with geodata in a GIS is to make sure that a common coordinate reference system (CRS) is used, both for the data itself and the current QGIS-project you are working in. For more info, see `here <https://docs.qgis.org/2.18/en/docs/gentle_gis_introduction/coordinate_reference_systems.html>`__. It is strongly recommended to reproject/transform all geodatasets into the same projected coordinate system before any processing starts. 


.. list-table::
   :widths: 20 20 30 30
   :header-rows: 1

   * - Topic
     - Parts of UMEP
     - Name
     - Application
   * - Source Area Footprint
     - Pre-Processor
     - `Footprint`
     - Interpretation of eddy covariance flux source areas
   * - Urban energy balance
     - Processor
     - `IntroductionToSuews`
     - Energy, water and radiation fluxes for one location
   * - Urban energy balance
     - Pre-Processor and Processor
     - `SUEWSAdvanced`
     - Energy, water and radiation fluxes for one location
   * - Urban energy balance
     - Pre-Processor, Processor and Post-processor
     - `SUEWSSpatial`
     - Energy, water and radiation fluxes for a spatial grid
   * - Urban energy balance
     - Pre-Processor, Processor and Post-processor
     - `SUEWSWUDAPT`
     - Making use of `WUDAPT <http://www.wudapt.org/>`__ local climate zones in `SUEWS  <http://suews-docs.readthedocs.io>`__
   * - Urban energy balance
     - Pre-Processor, Processor and Post-processor
     - `SUEWSWUDAPT_Beijing`
     - Making use of `WUDAPT <http://www.wudapt.org/>`__ local climate zones as well as `WATCH <http://www.eu-watch.org/>`__ meteorological forcing data in `SUEWS  <http://suews-docs.readthedocs.io>`__
   * - Solar Energy
     - Processor and Post-Processor
     - `SEBE`
     - Amount of solar energy received on building facets
   * - Outdoor thermal comfort
     - Pre-Processor and Processor
     - `IntroductionToSOLWEIG`
     - Mean radiation temperature modelling in complex urban settings
   * - Anthropogenic heat
     - Processor
     - `GQF`
     - Anthropogenic heat modelling in London using GQF (uses the GreaterQF methodology)

   * - Anthropogenic heat
     - Processor
     - `LQF`
     - Anthropogenic heat modelling in London using LQF (uses the LUCY methodology)




.. toctree::
   :caption: UMEP Tutorials
   :maxdepth: 2
   :hidden:

   Tutorials/Footprint
   Tutorials/IntroductionToSuews
   Tutorials/SuewsAdvanced
   Tutorials/SuewsSpatial
   Tutorials/SuewsWUDAPT
   Tutorials/SUEWSWUDAPT_Beijing
   Tutorials/IntroductionToSolweig
   Tutorials/SEBE
   Tutorials/LQF
   Tutorials/GQF
