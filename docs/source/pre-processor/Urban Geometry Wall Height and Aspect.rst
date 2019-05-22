.. _WallHeightandAspect:

Urban Geometry: Wall Height and Aspect
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Contributor:
    .. list-table::
       :widths: 50 50
       :header-rows: 1

       * - Name
         - Institution

       * - Fredrik Lindberg
         - Gothenburg


* Introduction:
    The wall height and aspect pre-processor can be used to identify wall pixels and their height from ground and building digital surface models (DSM) by using a filter as presented by Lindberg et al. (2015a). Optionally, wall aspect can also be estimated using a specific linear filter as presented by Goodwin et al. (1999) and further developed by Lindberg et al. (2015b) to obtain the wall aspect. Wall aspect is given in degrees where a north facing wall pixel has a value of zero. The output of this plugin is used in other UMEP plugins such as SEBE (Solar Energy on Building Envelopes) and height to width ratio.

* Dialog box
    .. figure:: /images/WallHeight.png
        :align: center

        The dialog for the Wall Height and Aspect calculator

* Building and Ground DSM:
    A DSM (geoTIFF) consisting of ground and building heights.

* Calculate Wall Aspect:
    Tick this box if you want to include estimation and output of a wall aspect grid. This calculation is computational intensive and will make your computer work for a while (depending on the size of the input DSM).

* Lower Limit for Wall Height (m):
    This limit gives the lowest height of a building wall.

* Output File for Wall Aspect Raster:
    Name of the output file of the aspect raster.

* Output File for Wall Height Raster:
    Name of the output file of the aspect raster.

* Run:
    Starts the calculations.

* Add Result to Project:
    If ticked, raster(s) will be added to the map canvas.

* Close:
    Closes the plugin.

* Output:
    Two different files (geoTIFF) will be saved if wall aspect is calculated.

* Example:
    .. figure:: /images/Output_Wall_Height.jpg
        :align: center
    
        A DSM (right) and resulting height raster (left).


* Remarks：
          - This plugin make use of **Scipy** which in turn make use of **Pillow**. If this plugin is malfunctioning, try to install/reinstall these packages (see `here <http://umep-docs.readthedocs.io/en/latest/Getting_Started.html#adding-missing-python-libraries-and-other-osgeo-functionalities>`__).
          -  **NOTE**: The azimuth of the wall is estimated based on a 9 meter linear feature. This implies that coarser pixel resolution gives less pixels and thus a more imprecise measure of wall azimuth as the number of pixels will be lower. It it therefore recommended that use pixel resolution not greater than 2 meter in order to obtain a reasonable result.
          -  Wall pixels will be located ‘outside’ of the building footprint.
          -  The aspect algorithm gives reasonable result but improvements could be made by e.g. using a vector line layer which could be used to populate the wall pixels with aspect values.
          -  **NOTE**: QGIS scales loaded rasters by a *cumulative count out* approach (98%). As the height and aspect layers are filled with zeros where no wall are present it might appear as there is no walls identified. Rescale your results to see the wall identified (*Layer Properties > Style*).

* References：
          -  Goodwin NR, Coops NC, Tooke TR, Christen A, Voogt JA (2009) Characterizing urban surface cover and structure with airborne lidar technology. `Can J Remote Sens 35:297–309 <http://www.tandfonline.com/doi/abs/10.5589/m09-015>`__
          -  Lindberg F., Grimmond, C.S.B. and Martilli, A. (2015a) Sunlit fractions on urban facets - Impact of spatial resolution and approach `Urban Climate DOI: 10.1016/j.uclim.2014.11.006 <http://www.sciencedirect.com/science/article/pii/S221209551400090X>`__
          -  Lindberg F., Jonsson, P. & Honjo, T. and Wästberg, D. (2015b) Solar energy on building envelopes - 3D modelling in a 2D environment `Solar Energy 115 369–378 <http://www.sciencedirect.com/science/article/pii/S0038092X15001164>`__
