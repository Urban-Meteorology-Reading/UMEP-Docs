.. _DailyShadowPattern:

Solar Radiation: Daily Shadow Pattern
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Fredrik Lindberg
     - Gothenburg


* Introduction:
     -  The **Shadow generator** plugin can be used to generate pixel wise shadow analysis using ground and building digital surface models (DSM). Optionally, vegetation DSMs could also be used. The methodology that is used to generate shadows originates from Ratti and Richens (1990) and is further developed and described in Lindberg and Grimmond (2011). Position of the Sun is calculated using **PySolar**, a python library for various Sun related applications ([2](http://pysolar.org/)).

* Dialog box ：
      .. figure:: /images/Shadow_generator.jpg

          The dialog for the ShadowGenerator

* Dialog sections：
      .. list-table::
         :widths: 10 90
         :header-rows: 0

         * - top
           - input data is specified
         * - middle
           - setting for positioning the Sun on the hemisphere
         * - bottom
           - to specify the output and to run the calculations

* Building and Ground DSM:
     - A DSM consisting of ground and building heights. This dataset also decides the latitude and longitude used for the calculation of Sun position.

* Vegetation Canopy DSM:
     - A DSM consisting of pixels with vegetation heights above ground. Pixels where no vegetation is present should be set to zero.

* Vegetation Trunk Zone DSM:
     - A DSM (geoTIFF) consisting of pixels with vegetation trunk zone heights above ground. Pixels where no vegetation is present should be set to zero.

* Use vegetation DSMs:
     - Tick this box if you want to include vegetation (trees and bushes) when shadows are generated.

* Trunk Zone DSM Exist:
     -  Tick this in if a trunk zone DSM already exist.

* Transmissivity of Light Through Vegetation (%):
     -  Percentage of light that is penetrating through vegetation. Default value is set to 3 % according to Konarska et al. (2013).

* Percent of Canopy Height:
     -  If a trunk zone vegetation DSM is absent, this can be generated based on the height of the Canopy DSM. The default percentage is set to 25%.

* Specify Data:
     -  The data need to be set in the middle section.

* Cast Shadows Only Once:
     -  Tick this box if you only want to cast one shadow. Below this tick box you can set the time that is needed to decide the position of the sun.

* Time Interval between Casting of each Interval:
     -  If the above tick box (Cast shadows only once) is not ticked in, a number of shadows is generated based on the interval set.

* UTC Offset (Hours):
     -  Time zone needs to be specified. Positive numbers moving east(e.g. Stockholm UTC +1).

* Output Folder:
     - A specified folder where the result will be saved.

* Run:
     - Starts the calculations

* Add Results to Project:
     -  If ticked, the shadow raster will be added to the map canvas.

* Close:
     - Closes the plugin.

* Output:
     -  If only one shadow image is generated, one geoTIFF will be produced where pixel values of zero indicates shadow and one indicates sunlit. If daily shadow casting is used (Cast shadows only once ticked off), one shadow image for each time step as well as one shadow fraction image is generated. The shadow fraction image is given in percent where 100% meaning the a pixel is sunlit throughout the day used in the calculation.

* Example of input data and result: 
.. figure:: /images/Shadow2.jpg

 shadow image in Gothenburg (1 m resolution), Sweden at 1 pm on the 2nd of October 2015 (daylight savings time).

* Remarks：
            -  All DSMs need to have the same extent and pixel
            -  This plugin is computationally intensive i.e. large grids will take a lot of time and very large grids will not be possible to use. Large grids e.g. larger than 4000000 pixels should be tiled before.


* References ：
      -  Konarska J, Lindberg F, Larsson A, Thorsson S, Holmer B 2013. Transmissivity of solar radiation through crowns of single urban trees—application for outdoor thermal comfort modelling. `Theoret. Appl. Climatol., 1–14 <http://link.springer.com/article/10.1007/s00704-013-1000-3>`__
      -  Lindberg, F., Grimmond, C.S.B., 2011a. The influence of vegetation and building morphology on shadow patterns and mean radiant temperatures in urban areas: model development and evaluation. `Theoret. Appl. Climatol. 105, 311–323 <http://link.springer.com/article/10.1007/s00704-010-0382-8>`__
      -  Ratti CF, Richens P (1999) Urban texture analysis with image processing techniques. In: Proceedings of the CAADFutures99, Atalanta, GA
