.. _SkyViewFactorCalculator:

Urban Geometry: Sky View Factor Calculator
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg
   * - Sue Grimmond
     - Reading



* Introduction:
     -  The Sky View Factor plugin can be used to generate pixel wise sky view factor (SVF) using ground and building digital surface models (DSM). Optionally, vegetation DSMs could also be used. By definition, SVF is the ratio of the radiation received (or emitted) by a planar surface to the radiation emitted (or received) by the entire hemispheric environment (Watson and Johnson 1987). It is a dimensionless measure between zero and one, representing totally obstructed and free spaces, respectively. The methodology that is used to generate SVF here is described in Lindberg and Grimmond (2010).


* Dialog box:
    .. figure:: /images/SVFCalculator.png

        The dialog for the Sky View Factor calculator

* Dialog sections:
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - top
     - Specify input data
   * - bottom
     - Specify output data and run calculation

* Building and Ground DSM:
     - A DSM (geoTIFF) consisting of ground and building heights.

* Vegetation Canopy DSM:
     - A DSM (geoTIFF) consisting of pixels with vegetation heights above ground. Pixels where no vegetation is present should be set to zero.

* Vegetation Trunk Zone DSM:
     - A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground. Pixels where no vegetation is present should be set to zero.

* Use Vegetation DSMs:
     - Tick this box if you want to include vegetation (trees and bushes) in the final SVF.

* Trunk Zone DSM Exist:
     -  Tick this box if a trunk zone DSM already exists.

* Transmissivity of Light Through Vegetation (%):
     -  Percentage of light that is penetrating through vegetation. The default value is set to 3 % according to Konarska et al. (2013).

* Percentage of Canopy height:
     - If a trunk zone vegetation DSM is absent, this can be generated based on the height of the Canopy DSM. The default percentage is set to 25%.

* Output Folder:
     - Specify folder where results will be saved.

* Run:
     - Starts the calculations.

* Add Result to Project:
     - If ticked, the total SVF raster will be added to the map canvas.

* Close:
     - Closes the plugin.

* Output:
     -  16 files (geoTIFF) will be saved if vegetation DSM is used. Otherwise, 5 SVFs are saved.
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - File
     - Description
   * - SkyViewFactor.tif
     - Total SVF, i.e. amount of sky that is seen from each pixel.
   * - SVF different directions
     - Four cardinal points
   * - SVF based on various fractions
     - Only buildings, only vegetation etc. For a detailed description, see Lindberg and Grimmond (2011).

* Example:
      .. figure:: /images/Output_Skyview.jpg

          Example of (left) input data - ground and building DSM (grayscale), DSM overlaid with a canopy DSM (yellow to green). Right: the resulting SVF -light highest SVF

* Remarks:

     -  All DSMs need to have the same extent and pixel size.
     -  This plugin is computationally intensive i.e. large grids will take a lot of time and very large grids will not be possible to use. Large grids e.g. larger than 4,000,000 pixels should be tiled before.

* References:
      -  Konarska J, Lindberg F, Larsson A, Thorsson S, Holmer B (2013). Transmissivity of solar radiation through crowns of single urban trees—application for outdoor thermal comfort modelling. `Theoret. Appl. Climatol., 1–14 <http://link.springer.com/article/10.1007/s00704-013-1000-3>`__
      -  Lindberg F, Grimmond CSB (2010) Continuous sky view factor maps from high resolution urban digital elevation models. `Clim Res 42:177–183 <http://www.int-res.com/abstracts/cr/v42/n3/p177-183/>`__
      -  Lindberg, F., Grimmond, C.S.B., 2011a. The influence of vegetation and building morphology on shadow patterns and mean radiant temperatures in urban areas: model development and evaluation. `Theoret. Appl. Climatol. 105, 311–323 <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
      -  Watson ID, Johnson GT (1987) Graphical estimation of skyview-factors in urban environments. `J Climatol 7: 193–197 <http://onlinelibrary.wiley.com/doi/10.1002/joc.3370070210/abstract>`__
