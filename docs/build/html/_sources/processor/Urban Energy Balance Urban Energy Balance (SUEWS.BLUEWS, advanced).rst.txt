.. _SUEWSadvanced:

Urban Energy Balance: Urban Energy Balance (SUEWS/BLUEWS, advanced)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg

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
      - `MetPreprocessor`, `WATCH`, `LandCoverReclassifier`, `LandCoverFraction(Point)`, `LandCoverFraction(Grid)`, `MorphometricCalculator(Point)`, `MorphometricCalculator(Grid)`, `SourceArea(Point)`

* Dialog box ：
      .. figure:: /images/SuewsAdvanced.png

          The dialog for SUEWS Advanced

* Dialog sections:
     -  When you run the plugin, you will see the dialog shown below. To use this plugin, all input data needs to be prepared beforehand. This can be done using the various plugins in the pre-processor in UMEP. The settings available in this plugin is used for specifying the settings for a specific model run. You should consult the manual (`1 <http://www.urban-climate.net/umep/SUEWS>`__) for instructions and information on what settings to use. For extensive models run it is recommended to execute the model outside of QGIS (see manual). The interface below creates a so-called namelist (**RunControl.nml**) that is used be the model for general settings. After running the model, this file can be found in the suewsmodel directory in the UMEP plugin directory.

* References:
      -  Järvi L, Grimmond CSB & Christen A (2011) The Surface Urban Energy and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver `J. Hydrol. 411, 219-237. <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
      -  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB (2014) Development of the Surface Urban Energy and Water balance Scheme (SUEWS) for cold climate cities, Geosci. Model Dev. 7, 1691-1711, `doi:10.5194/gmd-7-1691-2014 <http://www.geosci-model-dev.net/7/1691/2014/>`__.                                                                                                                                                                                                                                                                        |
      -  Ward HC, L Järvi, S Onomura, F Lindberg, CSB Grimmond (2016a) `SUEWS Manual <http://urban-climate.net/umep/SUEWS>`__: Version 2016a
      -  Ward HC. S Kotthaus, L Järvi, CSB Grimmond (2016b) Surface Urban Energy and Water Balance Scheme (SUEWS): development and evaluation at two UK sites `Urban Climate (in press) <:File:SUEWS_UKEvaluationPaper_Revised_v1-03.pdf>`__.
