.. _SUEWSSimple:

Urban Energy Balance: Urban Energy Balance (SUEWS, simple)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
 .. list-table::
    :widths: 50 50
    :header-rows: 0

    * - Name
      - Institution
    * - Fredrik Lindberg
      - Gothenburg
    * - Sue Grimmond
      - Reading

 * Introduction：
        - SUEWS can be run as a standalone or via UMEP (see `SUEWS Manual <SUEWS>`).
        - This plugin makes it possible to run a simplified version of the Surface Urban Energy and Water Balance Scheme (SUEWS). For a full version of the model, the SUEWS/BLUEWS (Advanced) plugin can be used. It is also available as a separate program.
        - SUEWS (Järvi et al. 2011, 2014, Ward et al. 2016a, b) simulates the urban radiation, energy and water balances using commonly measured/modeled meteorological variables and information about the surface cover. It utilizes an evaporation-interception approach (Grimmond et al. 1991), similar to that used in forests, to model evaporation from urban surfaces.
        - The model uses seven surface types: paved, buildings, evergreen trees/shrubs, deciduous trees/shrubs, grass, bare soil and water. The surface state for each surface type at each time step is calculated from the running water balance of the canopy where the evaporation is calculated from the Penman-Monteith equation. The soil moisture below each surface type (excluding water) is taken into account.
        - The model distributed with this manual can be run in two standard ways:
              -  For an individual area
              -  For multiple areas that are contiguous. There is no requirement for the areas to be of any particular shape but here we refer to them as ‘grids’.
        - Model applicability: Local scale – so forcing data should be above the height of the roughness elements (trees, buildings). SUEWS Simple is designed to be executed for a single location but the model is also able to be executed on a grid.

* Related Preprocessors：
      -  `MetaPreprocessor`, `WATCH`, `LandCoverReclassifier`, `LandCoverFraction(Point)`, `MorphometricCalculator(Point)`, `SourceArea(Point)`

* Dialog Box：
    .. figure:: /images/SuewsSimple.png

        Dialog for the SUEWS Simple plugin

* Dialog sections：
      .. list-table::
         :widths: 10 90
         :header-rows: 0

         * - far right
           - provides some tips and tricks for running the model.
         * - other four
           - to specify user-defined input data, either manually or by using the appropriate UMEP-plugin in the per-processor.
         * - bottom
           - to make some additional settings as well as running the model.

* Prepared dataset:
    SUEWS Simple comes with a prepared dataset that can be used for testing. This can be utilized by pressing **Add settings from test dataset**. This dataset is a fictitious dataset from the central parts of London.

* Building Morphology:
     - The three site specific building morphology parameters needed are usually derived from Digital Surface Models DSMs. However, they also can be entered manually.
     
           -  To use an already generated text file from the Image Morphometric Calculator (Point) plugin.
           -  To open the plugin from SUEWS Simple and generate the data.
     -  If an already generated text file is used, the **isotropic file** should be used (see Image Morphometric Calculator (Point)).

* Tree Morphology:
     -  Three site specific tree morphology parameters need to be specified. These can be derived from a Canopy DSMs that include vegetation heights. This can be entered manually or from the Image Morphometric Calculator (Point) plugin. When the plugin is used there are two options:
     
              -  To use an already generated text file from the Image Morphometric Calculator (Point) plugin.
              -  To open the plugin from SUEWS Simple and generate the data.
     -  If an already generated text file is used, the **isotropic file** should be used (see Image Morphometric Calculator (Point)).

* Land Cover Fractions ：
    Land cover fractions should add up to a total of 1. Values can be derived from a UMEP land cover dataset which can be generated via the Land Cover Reclassifier plugin in UMEP. The values can be entered manually or directly from the Land Cover Fraction (Point) plugin. If the plugin is used, there are two options:
    
       - To use an already generated text file from the Land Cover Fraction (Point) plugin.
       - To open the plugin from SUEWS Simple and generate the data.

* Initial Conditions:
    The initial conditions are entered here. These relate to time of year, days since rain, soil moisture state and daily mean air temperature at the beginning of a model run. The state of the leaf cycle sets a rough estimate of leaf area index based on season. To adjust this in more detail, the SUEWS, BLUEWS (Advanced) plugin should be used.

* Meteorological File:
    The location and filename (.txt) of the meteorological file should be specified here. The format used in most UMEP-related plugins where meteorological data is required can be generated using the Metdata Processor in UMEP. For details, see the help section in the Metdata Processor or the SUEWS manual (Ward et al. 2016a).

* Output Folder:
     - Specify a folder where you would like all the model results to be saved to. Make sure that you have write capabilities to the specified folder.
     - *Note if you put it within the UMEP plugin folder– be careful that you do not lose any results if you update the plugin by deleting it first.*

* Year:
    Specify what year you are running.

* Latitude:
    Specify the latitude in decimal degrees. Positive numbers indicate Northern Hemisphere.

* Longitude:
    Specify the longitude in decimal degrees. Positive numbers are to the West.

* Population Density:
    Specify the population density in people/ha (hectare) around the area of interest.

* Show Basic Plots of Model Results:
    Tick this box in if you would like to generate some simple plots of the result from a model run. This requires that the matplotlib library is added to your QGIS installation.

* Add Settings from Test Dataset:
    This is recommended if you want to try the model for the first time. This uses a year long dataset from London, UK.

* Run:
    Button starts the model. All inputs must be set prior to this button being available.

* Close:
     -  Button closes the plugin.

* References:
      -  Järvi L, Grimmond CSB & Christen A (2011) The Surface Urban Energy and Water Balance Scheme (SUEWS): Evaluation in Los Angeles and Vancouver `J. Hydrol. 411, 219-237. <http://www.sciencedirect.com/science/article/pii/S0022169411006937>`__
      -  Järvi L, Grimmond CSB, Taka M, Nordbo A, Setälä H &Strachan IB (2014) Development of the Surface Urban Energy and Water balance Scheme (SUEWS) for cold climate cities, Geosci. Model Dev. 7, 1691-1711, `doi:10.5194/gmd-7-1691-2014 <http://www.geosci-model-dev.net/7/1691/2014/>`__.                                                                                                                                                                                                                                                                        |
      -  Ward HC, L Järvi, S Onomura, F Lindberg, CSB Grimmond (2016a) `SUEWS Manual <SUEWS>`: Version 2016a
      -  Ward HC. S Kotthaus, L Järvi, CSB Grimmond (2016b) Surface Urban Energy and Water Balance Scheme (SUEWS): development and evaluation at two UK sites `Urban Climate (in press) <:File:SUEWS_UKEvaluationPaper_Revised_v1-03.pdf>`__.
