.. _Footprint:
Footprint
-------------

Introduction
~~~~~~~~~~~~~~~~~

Each meteorological instrument has a ‘\ *source area*\ ’ (sometimes
referred to as *footprint*), the area that influences the measurement.
The shape and location of that area is a function of the meteorological
variable the sensor measures and the method of operation of the sensor.

For turbulent heat fluxes measured with a sonic anemometer, extensive
effort has been directed to try and model the ‘probable source area
location’ (Leclerc and Foken 2014). Numerous models exist, but the
Kormann and Meixner (2001) and Kljun et al. (2015) models are used in
UMEP. Both models require input of information about the wind direction,
stability, turbulence characteristics (friction velocity, variance of
the lateral or crosswind wind velocity) and roughness parameters. Kljun
et al. (2015) requires the boundary layer height.

    .. figure:: /images/ReadingSourceArea.png

Initial Practical steps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  If **QGIS** is not on your computer you will `need to install
   it <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__
-  Then install the `**UMEP**
   plugin <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__

-  Start the QGIS software
-  If not visible on the desktop use the **Start** button to find the
   software (i.e. Find QGIS under your applications)
-  Select **QGIS 2.16.3 Desktop** (or the latest version installed)

When you open it on the top toolbar you will see **UMEP**.
|UMEP\_location.png|

-  If UMEP is not on your machine, download and install the `**UMEP**
   plugin <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__

-  Read through the section in the `online
   manual <http://urban-climate.net/umep/UMEP_Manual#Pre-Processor:_Urban_Morphology:_Source_Area_.28Point.29>`__
   BEFORE using the model, so you are familiar with it’s operation and
   terminology used.

Data for Tutorial
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use the appropriate data a) Reading -- `Download BB - week
5 <https://www.bb.reading.ac.uk>`__ or
`here <http://www.urban-climate.net/UMEPTutorials/Reading/DataReading.zip>`__
b) London -
`download <http://www.urban-climate.net/UMEPTutorials/London/DataSmallAreaLondon.zip>`__

`To get the Password if not given it
already <https://docs.google.com/forms/d/e/1FAIpQLSfH8eEly28SjtfvooWtJe95iRvLNV2tewNa3ZajrVFTXMKIfQ/viewform?formkey=dExvc3V1RDBqWmlIcURfLW5VOGtvQ0E6MQ&ifq>`__

Prior to Starting
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Read through the section in the `online
   manual <http://urban-climate.net/umep/UMEP_Manual#Pre-Processor:_Urban_Morphology:_Source_Area_.28Point.29>`__
   BEFORE using the model, so you are familiar with it’s operation and
   terminology used:
#. Download the **Data needed for the Tutorial** - you will be told
   which the appropriate data are:

   -  Reading -- `Download BB - week
      5 <https://www.bb.reading.ac.uk/>`__ or
      `here <http://www.urban-climate.net/UMEPTutorials/Reading/DataReading.zip>`__
   -  London -
      `download <http://www.urban-climate.net/UMEPTutorials/London/DataSmallAreaLondon.zip>`__

#. Load the Raster data (DEM, DSM,
   CDSM
   files – DOES A CDSM EXIST? Yes for London, No for Reading

   -  Go to: Layer > Add layer > Add Raster Layer > Locate downloaded
      files

        .. figure:: /images/Add_Raster_Layer.png


-  Have a look at the **layers** (see lower left) - if you untick the
   box filenames from the top you can see the different layers.

      .. figure:: /images/750px-Footprint1.png



Source Area Modelling
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. To access the Source area model or Footprint model:

   -  UMEP -> Pre-processor > Urban Morphology > Source Area Model
      (Point)

                .. figure:: /images/750px-Footprint1.png


           #. Click on *Select Point on Canvas* – then select a point (*e.g. where an Eddy Covariance (EC) tower site is located*)
           #. Select the appropriate surface elevation data file names
           #. Choose the model you wish to run (Kormann and Meixner 2001 or Kljun et al. 2015)
           #. Some initial parameters values are given `- think about what would be appropriate values for your site and period of interest <http://urban-climate.net/umep/UMEP_Manual#ConditionsAnchor>`__. The manual has more information (e.g. definitions) of the input variables.

             -   The values are dependent on the meteorological conditions and the surface surrounding the site. The former obviously vary on an hour to hour basis (or shorter time periods), whereas the others are dependent on the wind direction and the fetch characteristics.

           #. Add a prefix and an output folder.
           #. Tick “add the integrated source area to your project”. This will provide visual information of the location of the source area (footprint)
           #. Run - If you get an error/warning message (model is unable to execute your request - as the *maximum fetch exceeds the extent of your grid* for your point of interest. `measure the distance to the limit of your raster maps <Media:_MeasureTool.png>`__

             -   To allow the model to work for the dataset with your point of interest you need to adjust the maximum fetch distance.
             -   Locate the `Measure tool <Media:_MeasureTool.png>`__.
             -   Measure the distance to the point of interest to the boundary of the DSM data set.
             -   Adjust the maximum fetch.
             - - Click Run and wait for the calculations to finish.

           - The **output is a source area** grid showing the cumulative percentage of source area influencing the flux at the point of interest.

             -   To *display the legend*: Double-click on the source area grid and then click **OK** without doing any changes. The source area display is showing up to 98 % of the cumulative area.
             -   Other output: A **text file** giving both the input setting variables and the output morphometric parameters calculated based on the source area generated. More information is provided in the manual, `row titled: “Output” <http://urban-climate.net/umep/UMEP_Manual#ConditionsAnchor>`__

           - It is possible to **input a text file** to generate a source area based on morphometric parameters (e.g. an hourly dataset). However, for now you can moodify the input variables set in the interface. Format of file is given in the `manual <http://urban-climate.net/umep/UMEP_Manual#ConditionsAnchor>`__.


Iterative process
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To work with a site with no value known *a priori*.

#. Use the `Image
   Morphometric <http://urban-climate.net/umep/UMEP_Manual#Urban_Morphology:_Image_Morphometric_Parameters_Calculator_.28Point.29>`__
   Parameters Calculator (Point) tool in the UMEP plugin to select a
   point to get the initial parameter values:

   #. UMEP-> Pre-Processor -> Urban Morphology -> Image Morphometric
      Calculator
   #. Open the output files

#. **Anisotropic** file – has the values in, e.g., 5 degree **sectors**
   – i.e. what you selected. This is appropriate if the area is very
   inhomogeneous.
#. **Isotropic** file - has the **average value** for the area
#. Use these values to populate the source area model window.

Roughness parameters
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the UMEP plugin the roughness length and zero plane displacement
length can be calculated with a morphometric method based on the Rule of
Thumb (Grimmond and Oke 1999) as the default. There are other methods
available: Bottema (1995), Kanda et al. (2013), Macdonald et al. (1998),
Millward-Hopkins et al. (2011) and Raupach (1994, 1995). Many of these
have been developed for urban roughness elements. The Raupach method was
originally intended for forested areas but has also been found to
perform well for urban areas.

With wind profile and eddy covariance anemometric data and the source
area model, appropriate parameters can be determined and morphometric
methods assessed (e.g. Kent et al. 2017).

Questions for you to explore with UMEP: Source Area
---------------------------------------------------

#. What is the impact of the atmospheric and surface characteristics on
   the source area dimensions?
#. How do the source area characteristics vary for different sensor
   levels for the wind profile?

**Potential Projects**

#. How do the morphometric roughness methods compare with values
   obtained in the observatory? What is the influence of vegetation
   state?
#. Does wind direction impact the choice of the most appropriate method?
#. What is the difference in source area with models?
#. What inputs are the respective models most sensitive to?

References
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Bottema M 1995: Parameterisation of aerodynamic roughness parameters
   in relation to air pollutant removal efﬁciency of streets. Air
   Pollution Engineering and Management, H. Power et al., Eds.,
   Computational Mechanics, 235–242.
-  Grimmond CSB and TR Oke 1999: Aerodynamic properties of urban areas
   derived, from analysis of surface form. `Journal of Applied
   Climatology 38:9,
   1262-1292 <http://journals.ametsoc.org/doi/full/10.1175/1520-0450%281999%29038%3C1262%3AAPOUAD%3E2.0.CO%3B2>`__
-  Kanda M, Inagaki A, Miyamoto T, Gryschka M, Raasch S 2013: A new
   aerodynamic parameterization for real urban surfaces. `Boundary-
   Layer Meteorol 148:357–377.
   doi:10.1007/s10546-013-9818-x <http://link.springer.com/article/10.1007/s10546-013-9818-x?no-access=true>`__
-  Kent CW, Grimmond CSB, Barlow J, Gatey D, Kotthaus S, Lindberg F,
   Halios CH 2017: Evaluation of Urban Local-Scale Aerodynamic
   Parameters: Implications for the Vertical Profile of Wind Speed and
   for Source Areas. Boundary-Layer Meteorol 164:183-213.
-  Kljun N, Calanca P, Rotach MW, Schmid HP 2015: A simple
   two-dimensional parameterisation for Flux Footprint Prediction (FFP).
   `Geoscientific Model
   Development.8(11):3695-713. <http://www.geosci-model-dev.net/8/3695/2015/>`__
-  Kormann R, Meixner FX 2001: An analytical footprint model for
   non-neutral stratification. Bound.-Layer Meteorol., 99, 207–224
   http://www.sciencedirect.com/science/article/pii/S2212095513000497#b0145
-  Kotthaus S and Grimmond CSB 2014: Energy exchange in a dense urban
   environment – Part II: Impact of spatial heterogeneity of the
   surface. Urban Climate 10, 281–307
   http://www.sciencedirect.com/science/article/pii/S2212095513000497
-  Leclerc MY and Foken TK 2014: Footprints in Micrometeorology and
   Ecology. `Springer, xix, 239 p.
   E-book <http://www.springer.com/us/book/9783642545443>`__
-  Macdonald, R. W., R. F. Griffiths, and D. J. Hall, 1998: An improved
   method for estimation of surface roughness of obstacle arrays.
   `Atmos. Environ., 32,
   1857–1864 <http://www.sciencedirect.com/science/article/pii/S1352231097004032>`__
-  Millward-Hopkins JT, Tomlin AS, Ma L, Ingham D, Pourkashanian M 2011:
   Estimating aerodynamic parameters of urban-like surfaces with
   heterogeneous building heights. `Boundary-Layer Meteorol 141:443–465.
   doi:10.1007/s10546-011-9640-2 <http://link.springer.com/article/10.1007%2Fs10546-011-9640-2>`__
-  Raupach MR 1994: Simpliﬁed expressions for vegetation roughness
   length and zero-plane displacement as functions of canopy height and
   area index. `Bound.-Layer Meteor., 71, 211–216.
   doi:10.1007/BF0070922 <http://link.springer.com/article/10.1007%2FBF00709229>`__
-  Raupach MR 1995: Corrigenda. `Bound.-Layer Meteor., 76,
   303–304. <http://link.springer.com/article/10.1007/BF00709356>`__

Contributors to the material covered
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**University of Reading:** Christoph Kent, Simone Kotthaus, Sue Grimmond
**University of Gothenburg:** Fredrik Lindberg Background work also
comes from: UBC (Andreas Christen); Germany: Kormann and Meixner (2001);
Japan: Kanda et al. (2013); UK: Millward-Hopkins et al. (2011),
Macdonald et al. (1998); Australia: Raupach (1994, 1995); Netherlands:
Bottema (1995)

Authors of this document: Kent, Grimmond (2016). Lindberg

`UMEP Repository <https://bitbucket.org/fredrik_ucg/umep/>`__
