
Urban Land Cover: Land Cover Fraction (Grid)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - Fredrik Lindberg
     - Gothenburg
   * - Niklas Krave
     - Gothenburg



* Introduction:
      - The Land Cover Fraction (Grid) plugin calculates land cover fractions required for UMEP (see `Land Cover Reclassifier <#Urban_Land_Cover:_Land_Cover_Reclassifier>`__) from a point location based on a land cover raster grid. A land cover grid suitable for the processor in UMEP can be derived using the Land Cover Classifier. The fraction will vary depending on what angle (wind direction) you are interested in. Thus, this plugin is able to derive the land cover fractions for different directions. It is the same as the Land Cover Fraction (Point) except that this plugin calculates the fractions for each polygon object in polygon vector layer. The polygons should preferable be squares or any other regular shape. To create such a grid, built in functions in QGIS can be used (see *Vector -> Research Tools -> Vector Grid...*).   |

* Location:
  - The Land Cover Fraction (Grid) is located at
      -  UMEP
        -  Pre-Processor
          -  Urban Morphology
            -  Land Cover Fraction (Grid)

* Dialog Box:
      .. figure:: /images/LandCoverFractionGrid2.png

* Dialog sections：
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - upper
     - Sets the parameters for the area of interest where the fractions are calculated. You also set the search interval in degrees and from where the search should take place within each grid.
   * - middle
     - Specifies the input data regarding polygon layer and the land cover raster grid that should be used.
   * - lower
     - Specifies output and runs the calculations.

* Search Throughout the Grid Extent :
     - Select if the search should be performed from one side of the grid to the opposite side. Select the other option (Search from Grid Centroid) if the search should start from the centroid of the grid. Setting the **Search distance** can then allow for the search to extent beyond the grid. See the figure below for illustration. The left performs a search using the grid extent whereas the right illustrates a search from the centroid and extending outside of the grid.

     .. figure:: /images/Grid_Extent.png

* Wind Direction Search Interval (Degrees):
     -  This decides the interval in search directions for which the morphometric parameters will be calculated.

* Vector Polygon Grid:
     - Here the grid polygon layer should be specified.

* ID Field:
     -  Choose an attribute from the selected polygon layer that will be used to separate the different polygon objects from each other. An attribute field of unique numbers or letters should be used.

* Add results to polygon grid:
     - Tick this in if you would like to save a isotropic results in the attribute table for your polygon vector grid.

* UMEP Land Cover Grid:
     -  An integer raster land cover grid (e.g. geoTIFF) consisting of the various land covers specified above.

* File Prefix:
     - A prefix that will be included in the beginning of the output files.

* Ignore NoData pixels:
     -  Tick this in if NoData pixels should be ignored and calculation of grid should be performed eventhough NoData pixels exists within that grid. Nodata pixels are set to bare soil (6).

* Output Folder:
     - A specified folder where result will be saved.

* Run:
     - Starts the calculations.

* Close:
     - Closes the plugin.

* Output:
    -  Two different files are saved after a successful run.
         #. **anisotropic** results: land cover fractions for each wind direction as specified are included.
         #. **isotropic** results: all directions are integrated into one value for each land cover fraction.
    - If the raster data includes no data values within a polygon object, this grid will not be considered in the calculation.

* Remarks：
      -  Polygon grids must be squared (or rectangular) and allinged with the CRS used. This will be fixed in future versions so that any shaped grid can be used (see issue #12 in the `repository <https://bitbucket.org/fredrik_ucg/umep/issues>`__).
                                                                                                                                                                                                                                                            |
