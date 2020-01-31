.. _ExtremeFinder:

Outdoor Thermal Comfort: ExtremeFinder
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Contributor
   .. list-table::
      :widths: 50 50
      :header-rows: 1

      * - Name
        - Institution
      * - Bei Huang
        - Reading
      * - Andy Gabey
        - Reading
      * - Fredrik Lindberg
        - Gothenburg

* Current Options
    Identifies extreme high events (e.g. Heat waves) and low events (e.g. Cold Waves). Designed primarily for temperature data (heat waves identified from daily maximum and mean T; cold waves from daily minimum), but can also be used to indicate potential high and low extremes in other meteorological variables.

* Data must be provided by the user, and can be
     -  Previously-downloaded ERA5 data in a NetCDF (*-scf.nc) file (this can be obtained from the ERA5 downloader)
     -  Other NetCDF (.nc) file containing sub-daily measurements, or daily maximum/mean/minimum values. Must contain a **'time**' dimension, and variable(s) with name(s) matching those being analysed using the ExtremeFinder.
     -  Text (.txt) file, daily T\ :sub:`max`, T\ :sub:`avg` or T\ :sub:`min` (`file sample <http://www.urban-climate.net/watch_data/data%20set%20sample.txt>`__: 1979-01-01 to 2009-12-31). Only temperature analysis can be performed using a text file.

* Method
         Basis for thresholds - set into Input.nml (namelist)
            -  `Meehl and Tebaldi (2004) <http://science.sciencemag.org/content/305/5686/994>`__: 81st, 97.5th
            -  `Fischer and Schär (2010) <http://www.nature.com/ngeo/journal/v3/n6/full/ngeo866.html>`__: 90th
            -  `Vautard et al. (2013) <https://link.springer.com/article/10.1007%2Fs00382-013-1714-z>`__: 90th
            -  `Schoetter et al. (2014) <https://link.springer.com/article/10.1007/s00382-014-2434-8>`__: 98th
            -  `Sirje Keevallik (2015) <http://www.kirj.ee/26593/?tpl=1061&c_tpl=1064>`__: 10th
            -  `A. K. Srivastava (2009) <http://onlinelibrary.wiley.com/doi/10.1002/asl.232/abstract>`__: 3 °C
            -  Busuioc et al. (2010): 5 °C

* Dialog box
    .. figure:: /images/Extremefinder3.png
        :align: center
           
        The interface for the ExtremeFinder plugin

* Steps to use
      #. Select climate data: The ExtremeFinder will use all the data available in its analysis. You will be prompted for a text (.txt) or NetCDF (.nc) file:

         -  *NetCDF file*: The latitude, longitude, start and end date boxes will be populated automatically, if the data is available in the NetCDF file.
         -  *Text file*: The latitude, longitude, start and end date boxes must be filled in by the user, as the information is needed in calculations:

            -  *Latitude* (degrees N) and *Longitude* (degrees E) are WGS84 co-ordinates
            -  *Start* and *end date* are inclusive and must match the data extent

      #. Select the *extreme event type* and the *calculation method*:

         -  Event types are either Extreme *high* (e.g. Heat wave) or *low* (e.g. Cold wave)
         -  There are several different ways to identify extremes, depending on the event type
         -  Choose the *meteorological variable* to analyse for extremes

            -  **Note:** The methods in the Extreme Finder are based on Tair and may not be appropriate for other variables

      #. Select Output File: A list of extreme events will be written to the file

         -  Note: this will be overwritten if not a new name

      #. Run: Performs the analysis

* Output: Extreme events (heat waves used as example below)
      #. Daily T\ :sub:`max` (or T\ :sub:`avg` / T\ :sub:`min`) with time (Y=Year, X=Month)

         -  Colour gives Temperature (see key)
         -  Yellow Box Highlights Heatwave (Coldwave) periods This loads the model interface dialog box:

              .. figure:: /images/525px-TMax1.jpg
                  :align: center

                  Heat/Cold wave periods

      #. Box plot of distribution of heat (cold) wave by year.

         -  whiskers =1.5\* IQR
         -  outliers
            - any data beyond the whiskers

              .. figure:: /images/525px-HW_Box.jpg
                  :align: center

                  Box-and-whisker plot of Heat/Cold wave days each year

      #. Number of heat (cold) waves days per year
      
            .. figure:: /images/525px-HWDays.jpg
                :align: center

                Histogram showing number of Heat/Cold wave days each year
