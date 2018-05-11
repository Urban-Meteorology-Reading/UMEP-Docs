Spatial Data: DSM Generator
~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Developer:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Nils Wallenberg
     - Gothenburg


* Introduction:
    - Digital Surface Models (DSMs) is not always available for the area you want to investigate. The **DSM Generator** can be used to create or alter a DSM by using information from a polygon building footprint layer where a building height attribute is available. An option to acquire building footprints, and also in some cases building height from [Open Street Map](http://www.openstreetmap.org) data, is also available.

* Location:
  - The DSM Generator is located at
      -  UMEP
        -  Pre-Processor
          -  Spatial Data
            -  DSM Generator

* Dialog box:
    .. figure:: /images/DSMGenerator.png

* Dialog sections:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - top
     - input DEM data is specified
   * - middle upper
     - input polygon with height data or OSM is specified
   * - middle
     - map extent is specified
   * - middle lower
     - to specify the output DSM and output resolution
   * - bottom
     - to run the calculations

* Digital Elevation Model:
    -  A raster file containing elevation values needed to create the DSM

* Polygon Vector File:
    -  A polygon vector file including height values of buildings needed to create the DSM

* Necessary attributes:
    - Building height values in meters

* Use Open Street Map:
    -  Tick this in if you do not have a polygon layer with building heights. Open Street Map (© OpenStreetMap contributors) data will be used instead. If no building height is found **building level height** will be used instead. Set to appropriate value, e.g. a three level building with building level height set to 3 will be 3 \* 3 = 9 meters high.

* Save OSM as shapefile:
    -  Tick this in if you want to save the Open Street Map data as a polygon layer. This can be used if you want to look at what values has been used and if you want to add values manually.

* Map extent:
    - Set either to map canvas extent or extent from layer. Extent have to be smaller or equal to the raster DEM extent specified in the top section.

* Digital Surface Model:
    -  Set output for the generated DSM. Also set output resolution.

* Run:
    -  Starts the calculations

* Close:
    -  Closes the plugin.

* Output:
    - One GeoTIFF is created, a DSM.

* Remarks:
    -  The DEM raster and map canvas should be in a projection with meters as units.
    -  Raster elevation data (DEM) can be retrieved from e.g. `OpenDEM <http://www.opendem.info/>`__.
    -  If you use Open Street Map make sure you read `Open Street Map <http://www.openstreetmap.org/copyright>`__ © OpenStreetMap contributors.
