Introduction
------------

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

.. figure:: ReadingSourceArea.png
   :alt:  Example result
   :width: 1100px

    Example result

Initial Practical steps
-----------------------

-  If **QGIS** is not on your computer you will `need to install
   it <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__
-  Then install the `**UMEP**
   plugin <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__

-  Start the QGIS software
-  If not visible on the desktop use the **Start** button to find the
   software (i.e. Find QGIS under your applications)
-  Select **QGIS 2.16.3 Desktop** (or the latest version installed)

When you open it on the top toolbar you will see **UMEP**.
|UMEP_location.png|

-  If UMEP is not on your machine, download and install the `**UMEP**
   plugin <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__

-  Read through the section in the `online
   manual <http://urban-climate.net/umep/UMEP_Manual#Pre-Processor:_Urban_Morphology:_Source_Area_.28Point.29>`__
   BEFORE using the model, so you are familiar with it’s operation and
   terminology used.

Data for Tutorial
~~~~~~~~~~~~~~~~~

Use the appropriate data

``a) Reading -- ``\ ```Download``\ ````\ ``BB``\ ````\ ``-``\ ````\ ``week``\ ````\ ``5`` <https://www.bb.reading.ac.uk>`__\ ``  or ``\ ```here`` <http://www.urban-climate.net/UMEPTutorials/Reading/DataReading.zip>`__

b) London -
`download <http://www.urban-climate.net/UMEPTutorials/London/DataSmallAreaLondon.zip>`__

`To get the Password if not given it
already <https://docs.google.com/forms/d/e/1FAIpQLSfH8eEly28SjtfvooWtJe95iRvLNV2tewNa3ZajrVFTXMKIfQ/viewform?formkey=dExvc3V1RDBqWmlIcURfLW5VOGtvQ0E6MQ&ifq>`__

Prior to Starting
-----------------

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

#. Load the Raster data (`DEM, DSM,
   CDSM <http://urban-climate.net/umep/UMEP_Manual#Abbreviations>`__)
   files – DOES A CDSM EXIST? Yes for London, No for Reading

   -  Go to: Layer > Add layer > Add Raster Layer > Locate downloaded
      files

.. figure:: Add_Raster_Layer.png
   :alt:  none

    none

-  Have a look at the **layers** (see lower left) - if you untick the
   box filenames from the top you can see the different layers.

.. figure:: ReadingMap.png
   :alt:  none
   :width: 1050px

    none

Source Area Modelling
---------------------

#. To access the Source area model or Footprint model:

   -  UMEP -> Pre-processor > Urban Morphology > Source Area Model
      (Point) `this appears like this <Media:UMEP_location.png>`__

+-----------+-----------+-----------+-----------+-----------+-----------+
| Image     | Steps     |
+===========+===========+
| [[File:Fo | 500px     | Figure]]  | #. Click  | measure   | Measure   |
| otprint1. |           |           |    on     | the       | tool]].   |
| png       |           |           |    *Selec | distance  |           |
|           |           |           | t         | to the    | #*Measure |
|           |           |           |    Point  | limit of  | the       |
|           |           |           |    on     | your      | distance  |
|           |           |           |    Canvas | raster    | to the    |
|           |           |           | *         | maps]]    | point of  |
|           |           |           |    – then |           | interest  |
|           |           |           |    select | #*To      | to the    |
|           |           |           |    a      | allow the | boundary  |
|           |           |           |    point  | model to  | of the    |
|           |           |           |    (*e.g. | work for  | DSM data  |
|           |           |           |    where  | the       | set.      |
|           |           |           |    an     | dataset   |           |
|           |           |           |    Eddy   | with your | #*Adjust  |
|           |           |           |    Covari | point of  | the       |
|           |           |           | ance      | interest  | maximum   |
|           |           |           |    (EC)   | you need  | fetch.    |
|           |           |           |    tower  | to adjust |           |
|           |           |           |    site   | the       | #*Click   |
|           |           |           |    is     | maximum   | Run and   |
|           |           |           |    locate | fetch     | wait for  |
|           |           |           | d*)       | distance. | the       |
|           |           |           | #. Select |           | calculati |
|           |           |           |    the    | #*Locate  | ons       |
|           |           |           |    approp | the       | to        |
|           |           |           | riate     | [[Media:  | finish.   |
|           |           |           |    surfac | MeasureTo |           |
|           |           |           | e         | ol.png    | The       |
|           |           |           |    elevat |           | **output  |
|           |           |           | ion       |           | is a      |
|           |           |           |    data   |           | source    |
|           |           |           |    file   |           | area**    |
|           |           |           |    names  |           | grid      |
|           |           |           | #. Choose |           | showing   |
|           |           |           |    the    |           | the       |
|           |           |           |    model  |           | cumulativ |
|           |           |           |    you    |           | e         |
|           |           |           |    wish   |           | percentag |
|           |           |           |    to run |           | e         |
|           |           |           |    (Korma |           | of source |
|           |           |           | nn        |           | area      |
|           |           |           |    and    |           | influenci |
|           |           |           |    Meixne |           | ng        |
|           |           |           | r         |           | the flux  |
|           |           |           |    2001   |           | at the    |
|           |           |           |    or     |           | point of  |
|           |           |           |    Kljun  |           | interest. |
|           |           |           |    et al. |           |           |
|           |           |           |    2015)  |           | -  To     |
|           |           |           | #. Some   |           |    *displ |
|           |           |           |    initia |           | ay        |
|           |           |           | l         |           |    the    |
|           |           |           |    parame |           |    legend |
|           |           |           | ters      |           | *:        |
|           |           |           |    values |           |    Double |
|           |           |           |    are    |           | -click    |
|           |           |           |    given  |           |    on the |
|           |           |           |    `-     |           |    source |
|           |           |           |    think  |           |    area   |
|           |           |           |    about  |           |    grid   |
|           |           |           |    what   |           |    and    |
|           |           |           |    would  |           |    then   |
|           |           |           |    be     |           |    click  |
|           |           |           |    approp |           |    **OK** |
|           |           |           | riate     |           |    withou |
|           |           |           |    values |           | t         |
|           |           |           |    for    |           |    doing  |
|           |           |           |    your   |           |    any    |
|           |           |           |    site   |           |    change |
|           |           |           |    and    |           | s.        |
|           |           |           |    period |           |    The    |
|           |           |           |    of     |           |    source |
|           |           |           |    intere |           |    area   |
|           |           |           | st <http: |           |    displa |
|           |           |           | //urban-c |           | y         |
|           |           |           | limate.ne |           |    is     |
|           |           |           | t/umep/UM |           |    showin |
|           |           |           | EP_Manual |           | g         |
|           |           |           | #Conditio |           |    up to  |
|           |           |           | nsAnchor> |           |    98 %   |
|           |           |           | `__.      |           |    of the |
|           |           |           |    The    |           |    cumula |
|           |           |           |    manual |           | tive      |
|           |           |           |    has    |           |    area.  |
|           |           |           |    more   |           | -  Other  |
|           |           |           |    inform |           |    output |
|           |           |           | ation     |           | :         |
|           |           |           |    (e.g.  |           |    A      |
|           |           |           |    defini |           |    **text |
|           |           |           | tions)    |           |    file** |
|           |           |           |    of the |           |    giving |
|           |           |           |    input  |           |    both   |
|           |           |           |    variab |           |    the    |
|           |           |           | les.      |           |    input  |
|           |           |           |           |           |    settin |
|           |           |           |    -  The |           | g         |
|           |           |           |       val |           |    variab |
|           |           |           | ues       |           | les       |
|           |           |           |       are |           |    and    |
|           |           |           |       dep |           |    the    |
|           |           |           | endent    |           |    output |
|           |           |           |       on  |           |    morpho |
|           |           |           |       the |           | metric    |
|           |           |           |       met |           |    parame |
|           |           |           | eorologic |           | ters      |
|           |           |           | al        |           |    calcul |
|           |           |           |       con |           | ated      |
|           |           |           | ditions   |           |    based  |
|           |           |           |       and |           |    on the |
|           |           |           |       the |           |    source |
|           |           |           |       sur |           |    area   |
|           |           |           | face      |           |    genera |
|           |           |           |       sur |           | ted.      |
|           |           |           | rounding  |           |    More   |
|           |           |           |       the |           |    inform |
|           |           |           |       sit |           | ation     |
|           |           |           | e.        |           |    is     |
|           |           |           |       The |           |    provid |
|           |           |           |       for |           | ed        |
|           |           |           | mer       |           |    in the |
|           |           |           |       obv |           |    manual |
|           |           |           | iously    |           | ,         |
|           |           |           |       var |           |    `row   |
|           |           |           | y         |           |    titled |
|           |           |           |       on  |           | :         |
|           |           |           |       an  |           |    “Outpu |
|           |           |           |       hou |           | t” <http: |
|           |           |           | r         |           | //urban-c |
|           |           |           |       to  |           | limate.ne |
|           |           |           |       hou |           | t/umep/UM |
|           |           |           | r         |           | EP_Manual |
|           |           |           |       bas |           | #Conditio |
|           |           |           | is        |           | nsAnchor> |
|           |           |           |       (or |           | `__       |
|           |           |           |       sho |           |           |
|           |           |           | rter      |           | It is     |
|           |           |           |       tim |           | possible  |
|           |           |           | e         |           | to        |
|           |           |           |       per |           | **input a |
|           |           |           | iods),    |           | text      |
|           |           |           |       whe |           | file** to |
|           |           |           | reas      |           | generate  |
|           |           |           |       the |           | a source  |
|           |           |           |       oth |           | area      |
|           |           |           | ers       |           | based on  |
|           |           |           |       are |           | morphomet |
|           |           |           |       dep |           | ric       |
|           |           |           | endent    |           | parameter |
|           |           |           |       on  |           | s         |
|           |           |           |       the |           | (e.g. an  |
|           |           |           |       win |           | hourly    |
|           |           |           | d         |           | dataset). |
|           |           |           |       dir |           | However,  |
|           |           |           | ection    |           | for now   |
|           |           |           |       and |           | you can   |
|           |           |           |       the |           | moodify   |
|           |           |           |       fet |           | the input |
|           |           |           | ch        |           | variables |
|           |           |           |       cha |           | set in    |
|           |           |           | racterist |           | the       |
|           |           |           | ics.      |           | interface |
|           |           |           |           |           | .         |
|           |           |           | #. Add a  |           | Format of |
|           |           |           |    prefix |           | file is   |
|           |           |           |    and an |           | given in  |
|           |           |           |    output |           | the       |
|           |           |           |    folder |           | `manual < |
|           |           |           | .         |           | http://ur |
|           |           |           | #. Tick   |           | ban-clima |
|           |           |           |    “add   |           | te.net/um |
|           |           |           |    the    |           | ep/UMEP_M |
|           |           |           |    integr |           | anual#Con |
|           |           |           | ated      |           | ditionsAn |
|           |           |           |    source |           | chor>`__. |
|           |           |           |    area   |           |           |
|           |           |           |    to     |           |           |
|           |           |           |    your   |           |           |
|           |           |           |    projec |           |           |
|           |           |           | t”.       |           |           |
|           |           |           |    This   |           |           |
|           |           |           |    will   |           |           |
|           |           |           |    provid |           |           |
|           |           |           | e         |           |           |
|           |           |           |    visual |           |           |
|           |           |           |    inform |           |           |
|           |           |           | ation     |           |           |
|           |           |           |    of the |           |           |
|           |           |           |    locati |           |           |
|           |           |           | on        |           |           |
|           |           |           |    of the |           |           |
|           |           |           |    source |           |           |
|           |           |           |    area   |           |           |
|           |           |           |    (footp |           |           |
|           |           |           | rint)     |           |           |
|           |           |           |           |           |           |
|           |           |           | #Run - If |           |           |
|           |           |           | you get   |           |           |
|           |           |           | an        |           |           |
|           |           |           | error/war |           |           |
|           |           |           | ning      |           |           |
|           |           |           | message   |           |           |
|           |           |           | (model is |           |           |
|           |           |           | unable to |           |           |
|           |           |           | execute   |           |           |
|           |           |           | your      |           |           |
|           |           |           | request - |           |           |
|           |           |           | as the    |           |           |
|           |           |           | *maximum  |           |           |
|           |           |           | fetch     |           |           |
|           |           |           | exceeds   |           |           |
|           |           |           | the       |           |           |
|           |           |           | extent of |           |           |
|           |           |           | your      |           |           |
|           |           |           | grid* for |           |           |
|           |           |           | your      |           |           |
|           |           |           | point of  |           |           |
|           |           |           | interest. |           |           |
|           |           |           | [[Media:  |           |           |
|           |           |           | MeasureTo |           |           |
|           |           |           | ol.png    |           |           |
+-----------+-----------+-----------+-----------+-----------+-----------+

Iterative process
-----------------

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
~~~~~~~~~~~~~~~~~~~~

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
----------

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**University of Reading:** Christoph Kent, Simone Kotthaus, Sue Grimmond
**University of Gothenburg:** Fredrik Lindberg Background work also
comes from: UBC (Andreas Christen); Germany: Kormann and Meixner (2001);
Japan: Kanda et al. (2013); UK: Millward-Hopkins et al. (2011),
Macdonald et al. (1998); Australia: Raupach (1994, 1995); Netherlands:
Bottema (1995)

Authors of this document: Kent, Grimmond (2016). Lindberg

`UMEP Repository <https://bitbucket.org/fredrik_ucg/umep/>`__

.. |UMEP_location.png| image:: UMEP_location.png

