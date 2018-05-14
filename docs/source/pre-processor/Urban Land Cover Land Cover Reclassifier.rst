Urban Land Cover: Land Cover Reclassifier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg


* Introduction:
     -  The Land Cover Reclassifier is a simple plugin that can be used to create a UMEP land cover raster grid. The land cover fractions included in UMEP are:
.. list-table::
   :widths: 33 33 33
   :header-rows: 0

   * - 1
     - Paved
     - Paved surfaces (e.g. roads, car parks)
   * - 2
     - Buildings
     - Building surfaces
   * - 3
     - Evergreen Trees
     - Evergreen trees and shrubs
   * - 4
     - Deciduous Trees
     - Deciduous trees and shrubs
   * - 5
     - Grass
     - Grass surfaces
   * - 6
     - Bare soil
     - Bare soil surfaces and unmanaged land
   * - 7
     - Water
     - Open water (e.g. lakes, ponds, rivers, fountain)

* Location:
  - The Land Cover Reclassifier is located at
      -  UMEP
        -  Pre-Processor
          -  Urban Land Cover
            - Land Cover Reclassifier

* Dialog box:

        .. figure:: /images/Landcoverreclassifier.png

* Dialog sections:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - upper
     - Select raster land cover dataset to be reclassified into the UMEP land cover classes
   * - middle
     - Choose interval values to be classified into a certain UMEP land cover class.
        - Not all lines and boxes need to be filled in, but multiple lines are available in case many different intervals are to be classified as the same land cover class.
   * - lower
     - Specify the output file (.tiff) etc.

* Input raster:
     -  Any valid raster dataset (float or integer) loaded into QGIS will appear in this dropdown list. Choose the one that includes your land cover information.

* Land cover classes:
     -  Fill the interval values that you want to reclassify into a certain cover class. All values not included will appear as 0 in the output land cover raster. This should be avoided.

* Output file:
     - Location and filename (geoTIFF) are specified here.

* Run:
     - Starts the reclassification.

* Close:
     - Closes the plugin.
