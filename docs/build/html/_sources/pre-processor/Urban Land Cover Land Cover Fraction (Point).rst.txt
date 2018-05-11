
Urban Land Cover: Land Cover Fraction (Point)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg
   * - Niklas Krave
     - Gothenburg


* Introduction:
      - The Land Cover Fraction (Point) plugin calculates land cover fractions required for UMEP (see `Land Cover Reclassifier <#Pre-Processor:_Urban_Land_Cover:_Land_Cover_Reclassifier>`__) from a point location based on a land cover raster grid.
      - A land cover grid suitable for the processor in UMEP can be derived using the Land Cover Classifier. The fraction will vary depending on what angle (wind direction) you are interested in. Thus, this plugin is able to derive the land cover fractions for different directions.

* Location:
  - The Land Cover Fraction (Point) is located at
      -  UMEP
        -  Pre-Processor
          -  Urban Land Cover
            -  Land Cover Fraction (Point)

* Dialog box：
      .. figure:: /images/Land_Cover_Reclass.png

* Dialog section：
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - upper
     - Select a point on the map canvas by either clicking a location or selecting an existing point from a point vector layer.
   * - middle
     - Specify the area of interest where the morphometric parameters are calculated. Set the search interval in degrees.
   * - lower
     - Specify the input data regarding land cover fraction raster as well as specifying output and for running the calculations.


* Select Point on Canvas  :
     - Click to create a point from where the calculations will take place. When you click the button, the plugin will be disabled until you have clicked the map canvas.

* Use Existing Single Point Vector Layer:
     -  Select if you want to use a point from a vector layer that already exists and is loaded to the QGIS-project. The Vector point layer drop down list will be enabled and include all point vector layers available.

* Generate Study Area:
     - This button is connected to the Search distance (m). When you click it, a circular polygon layer (Study area) is generated. This is the area that will be used to obtain the land cover fractions.

* Wind Direction Search Interval (Degrees):
     -  This decides the interval in search directions for which the morphometric parameters will be calculated.

* UMEP Land Cover Grid:
     -  A integer raster land cover grid (e.g. geoTIFF) consisting of the various land covers specified above.

* File Prefix:
     - A prefix that will be included in the beginning of the output files.

* Output Folder:
     - Where the result will be saved.

* Run:
     - Starts the calculations.

* Close:
     - Closes the plugin.

* Output:
     -  Two different files are saved after a successful run.
          #. **anisotropic** results: land cover fractions for each wind direction as specified are included.
          #. **isotropic** results: all directions are integrated into one value for each land cover fraction.
