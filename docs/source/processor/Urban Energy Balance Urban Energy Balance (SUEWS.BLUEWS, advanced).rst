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

* Related Preprocessors:
      - `MetPreprocessor`, `WATCH`, `LandCoverReclassifier`, `LandCoverFraction(Point)`, `LandCoverFraction(Grid)`, `MorphometricCalculator(Point)`, `MorphometricCalculator(Grid)`, `SourceArea(Point)`

* Dialog box ：
      .. figure:: /images/SUEWSAdvanced_SuewsAdvanced.png

          The dialog for SUEWS Advanced

* Dialog sections:
     -  When you run the plugin, you will see the dialog shown above. To use this plugin, all input data needs to be prepared beforehand. This can be done using the various plugins in the pre-processor in UMEP (see `ToolApplications`). The settings available in this plugin is used for specifying the settings for a specific model run. You should consult the manual (`<http://suews-docs.readthedocs.io>`__) for instructions and information on what settings to use. 
     
     -  For extensive models run it is recommended to execute the model outside of QGIS (see manual). 
     
     -  The interface above creates a so-called namelist (**RunControl.nml**) that is used be the model for general settings. After running the model, this file can be found in the suewsmodel directory in the UMEP plugin directory as well as in the input folder specified.
     
     -  It is always recommended to make use of a spin-up period to adjust e.g. water availbility in the model. This can be dome by e.g. start your model before (months-years) the time period of interest. one option to use a spin-up procedure using exisitng data is availabe. This requires a full year meteorological dataset. This option will run the model for one year and then run the same year using the state from the first model run.

* References:
      -  Järvi L, Grimmond CSB & Christen A (2011) The Surface Urban Energy and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver `J. Hydrol. 411, 219-237. <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
      -  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB (2014) Development of the Surface Urban Energy and Water balance Scheme (SUEWS) for cold climate cities, Geosci. Model Dev. 7, 1691-1711, `doi:10.5194/gmd-7-1691-2014 <http://www.geosci-model-dev.net/7/1691/2014/>`__.                          
      -  Ward HC. S Kotthaus, L Järvi, CSB Grimmond (2016b) Surface Urban Energy and Water Balance Scheme (SUEWS): development and evaluation at two UK sites `link) <https://www.sciencedirect.com/science/article/pii/S2212095516300256>`__.
