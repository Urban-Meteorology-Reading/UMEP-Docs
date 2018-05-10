
Spatial Data: Tree Generator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Developer:
.. list-table::
   :widths: 50 50
   :header-rows: 0
   
   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg


* Introduction:
     - Information 3d vegetation is not a common spatial information available. The **Tree Generator** can be used to create or alter a vegetation CDSM and TDSM (see [abbreviations](http://urban-climate.net/umep/UMEP_Manual#Abbreviations)). Be using information from a point layer where the location of the points specifies the tree positions and the attributes sets the shape of the trees, it is possible to produce a the 3d vegetation needed for e.g. Mean radiant temperature modelling (SOLWEIG) or Urban Energy Balance modelling (SUEWS) in UMEP.

* Location:
  - The Tree Generator is located at
      -  UMEP
        -  Pre-Processor
          -  Spatial Data
            -  Tree Generator

* Dialog box:
    .. figure:: /images/Treegeneratorsolweig.png

* Dialog sections:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - top
     - input data is specified
   * - bottom
     - to specify the output and to run the calculations

* Point vector file:
     -  A point vector file including the appropriate attributes for generating the vegetation DSMs

* Necessary attributes:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - Tree type
     - Two different tree types (shapes) are currently included:
        - 1 = conifer
        - 2 = decidouos.
        - There is also a possibility to remove vegetation by setting tree type = 0 and with an appropriate diameter to remove all vegetation pixels from the DSMs.
   * - Total height
     - This is the total height of the tree from the ground (magl).
   * - Trunk height
     - This is the height up to the bottom of the canopy (magl).
   * - Diameter
     - This is the circular diameter of the tree in meter.

* Bollean building grid exist:
     -  Tick this in if a boolen building grid exist for your model domain. This can be generated from the SOLWEIG-plugin.

* Building and Ground DSM:
     -  A DSM consisting of ground and building heights.

* Ground DEM:
     - A DEM cosisting of ground heights.

* Building grid:
     -  A grid where building pixels are 0 and all other pixels are 1.

* Vegetation Canopy DSM:
     -  A DSM consisting of pixels with vegetation heights above ground.

* Vegetation Trunk Zone DSM:
     -  A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground.

* Output Folder:
     -  A specified folder where the result will be saved.

* Run:
     -  starts the calculations

* Close:
     -  closes the plugin.

* Output:
     - Two geoTIFFs are created, one CDSM and one TDSM.

* Remarks:
      -  All DSMs need to have the same extent and pixel

      -  To ceate a bush, set trunk height to

      -  The SOLWEIG plugin cn be used to create the boolean building grid as well as a TDSM based on a
