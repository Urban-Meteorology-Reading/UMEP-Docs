LQF Manual
################


Overview
--------

LQF provides a method to calculate the anthropogenic heat flux. It uses
wide-area energy consumption and vehicle ownership values, and uses and
higher-resolution residential population data estimate the heat flux
from buildings, transport and human metabolism at 60 minute intervals at
the spatial resolution of the population data.

-  Energy and vehicle use are assumed to be correlated to residential
   (night-time) populations
-  Temporal resolution is maximised by applying empirically measured
   diurnal, day-of-week and seasonal variations to the data.

Workflow to model Q\ :sub:`F`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Select parameters and data sources files
#. Select output path: This contains model outputs, logs and any
   pre-processed data that is produced
#. Perform pre-processing of the data or select existing pre-processed
   data: A single set of processed input data can be re-used in
   subsequent runs
#. Optionally: Specify land cover fractions at high spatial resolution:
   Allows the spatial resolution of the modelled outputs to be enhanced
#. Run the model: Executes the model for the chosen date range
   components.
#. Visualise outputs: A simple tool is provided to generate maps and
   time series from the model outputs.

Main user interface
-------------------

The main user interface allows the user to select the temporal extent of
the model run, and the configuration files. The configuration files
describe model assumptions and the library of available data files.

 **Running the model**

  .. figure:: /images/300px-LUCY_main.png

      LQF main dialogue box

 1: Specify model configuration files and output path:

 -  LQF needs spatial and temporal information about the population, energy consumption and transport in order to model Q\ :sub:`F` at high temporal and spatial resolution:

 -  Model parameters file `Parameters_file`_: Fortran-90 namelist file containing numerical parameters required in model calculations

 -  `Data sources file`_: Fortran-90 namelist file that contains the locations of spatial and temporal input files used by the model

 -  **Output Path**: Directory into which `Model outputs`_ and associated data will be stored. *Any existing files will be overwritten.*

 2: Input data is pre-processed:

 -  Before it can be used in the model, the wide-area energy use, vehicle ownership and population data in the data sources file must be (dis)aggregated using local population data to match the chosen output areas.

 -  Data is processed using the **Prepare input data using data sources** button. This performs disaggregation and saves the output files to the /DownscaledData/ subfolder of the chosen model output directory. This step can take up to several hours, during which QGIS will not respond to input.

 -  If processed input data already exists elsewhere it can be used instead by specifying the path using the **Available at:** box. The processed files are copied to the /DownscaledData/ subfolder of the chosen model output directory.

 -  Optional: **Extra disaggregation** uses an additional set of inputs so the data can be disaggregated to a higher spatial resolution:

    -  **Land cover fractions**: Land cover fractions calculated using the UMEP land cover classifier in the pre-processing toolbox.
    -  **Corresponding polygon grid**: The ESRI shapefile grid of polygons represented by the land cover fractions.
    -  **Grid cell ID field**: The field of the polygon grid shapefile that contains a unique identifier for each cell. This is used to cross-reference model outputs.

 3: Choose temporal domain:

 -  **Dates to model** (outputs are produced at 60-minute intervals). Either:

    -  **Date range**: The first and final dates are specified and the whole period is simulated.
    -  **Date list**: A comma-separated list of dates in YYYY-mm-dd format (e.g. 2015-01-02, 2016-03-05, 2014-05-03) is provided. These dates are simulated in their entirety.

 4: Run model and visualise results:

 -  The **Run Model** button executes the model, which applies the temporal disaggregations and calculates Q\ :sub:`F` components in each output area. This takes up to several hours for high resolution or long study periods. During this time QGIS will not respond to input.
 -  Results are visualised using the **Visualise...** button
 -  Previous model results are retrieved using the **Load Results** button, which allows a previous model output folder to be selected.

 Data are ready for use in Q\ :sub:`F` calculations after this point

 **Visualising output**

     .. figure:: /images/300px-Visualise.png

        LQF results visualisation dialogue box


     .. figure:: /images/300px-Timeseries.png

        Time series output example

 A simple visualisation tool accompanies the model which produces maps and time series plots of the available data.

 **Time series plots**

 -  One plot per output area is produced for all of the time steps present in the model output directory, showing the three Q\ :sub:`F` components on separate axes. To plot a time series, select the output area of interest and click the “Show plot” button. The plot areas can be manipulated and graphs exported using the tools in the plot window.

 **Maps**

 -  One map per Q\ :sub:`F` component and time step is produced, coloured on a logarithmic scale according to the Q\ :sub:`F` value in each output area. One or more LQF time steps is selected in the list, and every Q\ :sub:`F` component is displayed for each date in the QGIS window by pressing “Add to canvas”.

 Note: Rendering maps may take several minutes for high-resolution model results.


Model outputs
-------------

Model outputs are stored in the /ModelOutput/ subdirectory of the
selected model output directory. A separate data file is produced for
each time step of the model run. Each file contains four columns (one
each for total, building, transport and metabolism) and a row for each
output area.

-  Output files are timestamped with the pattern
   **LQFYYYYmmdd\_HH-MM**.csv, with times stated in UTC.

   -  YYYY: 4-digit year
   -  mm: 2-digit month
   -  dd: 2-digit day of month
   -  HH: 2-digit hour (00 to 23)
   -  MM: 2-digit minute

-  The first model output is labelled 01:00UTC and covers the period
   00:00-01:00 UTC.
-  Each data file is in comma-separated value (CSV) format

Synthesised shapefiles
----------------------

If pre-processing of the input data has taken place, the Disaggregated
energy, transport and population shapefiles are stored in the
**/DownscaledData/** subdirectory of the model outputs, with filenames
that reflect the time period they represent. This folder can be used as
the source of processed input data in future runs to save time, provided
that the data sources file has not changed.

If previously processed input data are being used, these are copied to
the **/DownscaledData/** subdirectory of the current model run

Logs
----

Several log files are saved in the **/Logs/** subdirectory. The logs are
intended to help interpretation of model outputs by providing a
traceable history of why a particular spatial or temporal disaggregation
value was looked up.

#. The steps taken to disaggregate spatial data, including which
   attributes were involved
#. The day of week and the time of day that was returned from each
   diurnal and annual profile data source when it was queried with a
   particular model time step.

Configuration files
-------------------

The Parameters and Data Sources file are copied to the **/ConfigFiles/**
subdirectory of the model output directory for future reference.

Input data
--------------

Input data consists of spatial and temporal information, a lookup table
for vehicle fuel efficiency and (optionally) land use cover data to
further enhance the spatial resolution of the model output.

Spatial information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wide-area data
^^^^^^^^^^^^^^^^^^^^^

An internal database contains nation-level parameters. These are
disaggregated and downscaled based on residential population data. Any
output areas spatially outside a territory will be labelled as belonging
to no nation, and therefore receive zero vehicles, energy consumption or
metabolism.

The database contains the following data for each country. Some of these
are time varying, which values stored for each year that data is
available (1950 onwards). The data can be added to using standard SQL
tools such as SQLite browser, the pandas package in Python or
open-source programming tools. Data can be added for any or all
time-varying quantities, and non-consecutive years are permitted. The
entries are as follows:

.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - Attribute
     - Description
     - Units

   * - kwh\_year
     - Total annual primary energy consumption (time-varying)
     - kWh per year
   * - motorcycles
     - Total motorcycle ownership (time varying)
     - Per 1,000 people
   * - cars
     - Total passenger car ownership (time varying)
     - Per 1,000 people
   * - freight
     - Total freight vehicles (time varying)
     - Per 1,000 people
   * - ecostatus
     - World Bank national income classification (1 to 4, 1 being highest)
     - -
   * - summer\_cooling
     - Whether summer cooling is a significant impact on energy consumption (1=Yes, 0=No)
     - -
   * - wake\_hour
     - Time when 50% of the population has woken up in the morning
     - Hour of day (local time)
   * - sleep\_hour
     - Time when 50% of the population has gone to sleep at night
     - Hour of day (local time)
   * - transition\_time
     - Timescale over which waking and sleeping occurs
     - Hours
   * - population
     - Total population (time-varying)
     - -
   * - fixedHolidays
     - Days of the year that contain fixed public holidays for each country (e.g. December 25 in the UK)
     - DOY (non-leap year. Adjusted values used when leap year modelled)
   * - weekendDays
     - The days of the week that are assumed as weekends in each country
     - 1 (weekend) or 0 (weekday)
   * - weekendCycles
     - Country-specific diurnal variation for weekend building energy consumption and traffic flow
     - Local time
   * - weekdayCycles
     - Country-specific diurnal variation for weekday building energy consumption and traffic flow
     - Local time


Time indexing of wide-area data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The model selects an appropriate time-varying value (e.g. population)
from the database as follows:

#. If the model time step is before the first available year, the model
   will report an error.
#. If the model time step is after the final available year, the latest
   value is used.
#. If the model time step is in between two available years, the earlier
   year is used.

Local data
^^^^^^^^^^

An ESRI shapefile containing spatially resolved population data. This is
used to disaggregate the wide-area totals and estimate metabolism across
the study area.

-  Since population data are key to the model method, it is important to
   use the finest available spatial scale.
-  The model must output results for a consistent set of spatial units,
   so the populations are assigned to the model output areas based on
   how much each spatial unit of population is intersected each output
   area. It is **recommended** that a population shapefile is chosen as
   the output areas.
-  The field containing the population must be labelled “Pop” in the
   shapefile attributes

Temporal information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Information needed by LQF
^^^^^^^^^^^^^^^^^^^^^^^^^

Temporal data allows the annualised data provided by the shapefiles to
be temporally disaggreated into time series. LQF requires daily and
hourly information:

#. **Daily information**: The mean daily temperature (degrees Celsius)
   for the region being studied, covering the period of study. The model
   estimates day-to-day changes in building energy consumption based on
   the daily mean temperature. The temperature input file for each year
   is provided by a file with 365 (or 366) entries.
#. **Hourly information**: Template diurnal cycles at 60-minute
   intervals for total energy consumption, total traffic flow, metabolic
   heat emitted per person and the proportion of the population emitting
   this heat.

   -  Variations of these cycles for different **days of week**
   -  Variations of the above at different **times of year** (if
      available)

#. *' Time zone information*': Temporal files must contain the time zone
   represented by the data file. Time zones are specified using the list
   of `https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones
   standard time zone
   names. <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones_standard_time_zone_names.>`__.

Metabolism is based purely on data in the LQF database and can't be
overridden. The LQF database contains one default diurnal profile for
traffic flow and building energy consumption, but these should be
overridden with local data files whenever possible:

.. list-table::
   :widths: 33 33 33
   :header-rows: 1

   * - Q\ :sub:`F` component
     - File description(s)
     - Size of file
   * - Transport
     - Traffic flows for each vehicle type during each day of the week
     - 7 days \* 24 hours \* N seasons
   * - Building
     - Building energy consumption during each day of the week
     - 7 days \* 24 hours \* N seasons


Each temporal file contains headers that store metadata used by the
model to interpret the data:

#. The time zone represented by the file
   (“`UTC <https://en.wikipedia.org/wiki/Coordinated_Universal_Time>`__\ ”
   or of the style “Europe/London”). If “UTC” is specified, then values
   must be explicitly provided for each daylight savings regime to
   capture shifts in human behaviour. Note that the model outputs are
   always UTC, with the necessary conversion taking place in the
   software.
#. The start and end dates of the period represented by the data. This
   allows seasonality to be captured.

Ideally these files contain data taken from the period being modelled,
but this is not always practical. In this case, temporal profile data
from the most recent available year is looked up for the same day of
week (taking into account public holidays), season and daylight savings
regime if applicable. Different variants are used for traffic, energy
and metabolism, and each of these is described below.

Details of temporal input files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Daily temperature
'''''''''''''''''

This file records daily air temperature, from which the model estimates
the response in building energy consumption. These are expressed in
degrees Celsius.

The file consists of Two columns. The first is the day of year; the
second is the temperature. The file must contain values for the days
from StartDate to EndDate (inclusive), and the column and row headers
must be identical to those shown.

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Data
     - T\_Celsius
   * - StartDate
     - 2015-01-01
   * - EndDate
     - 2015-12-31
   * - Timezone
     - Europe/London
   * - 1
     - 9.161881378
   * - 2
     - 9.582277749
   * - 3
     - 5.615161127
   * - 4
     - 3.62641677
   * - 5
     - 8.310810996
   * - 6
     - 8.237201333
   * - 7
     - 7.586860408

Diurnal variations
''''''''''''''''''

The same file format is used for both traffic flow and building energy
consumption. Each file contains 7 days of data at 1 hour resolution (168
rows). The first row represents the period 00:00-01:00 on Monday
morning, and the final row represents 23:00-00:00 on Sunday Evening
(into Monday).

The following header lines must be present:

-  **Season**: A name for the period represented by each column.
-  **Start Date**: The first day of the period (e.g. season) represented
   by the data
-  **End Date**: The final day of this period

Notes:

-  Periods are not allowed to overlap
-  The units of measurement are not important: The values within a given
   day are normalised after they are loaded into the model software

The example below shows the first 24 rows of a file that contains
entries for the 4 quarters of 2014. Any number of seasons/periods of
year can be added to a single file, and multiple files can be added.

.. list-table::
   :widths: 20 20 20 20 20
   :header-rows: 1

   * - Season
     - Q1
     - Q2
     - Q3
     - Q4
   * - StartDate
     - 2014-01-01
     - 2014-04-01
     - 2014-07-01
     - 2014-10-20
   * - EndDate
     - 2014-03-31
     - 2014-06-30
     - 2014-09-30
     - 2014-12-31
   * - Timezone
     - Europe/London
     -
     -
     -
   * - 01:00
     - 0.273
     - 0.294
     - 0.306
     - 0.287
   * - 02:00
     - 0.236
     - 0.248
     - 0.259
     - 0.242
   * - 03:00
     - 0.228
     - 0.238
     - 0.24
     - 0.228
   * - 04:00
     - 0.219
     - 0.228
     - 0.227
     - 0.222
   * - 05:00
     - 0.226
     - 0.226
     - 0.227
     - 0.222
   * - 06:00
     - 0.254
     - 0.245
     - 0.238
     - 0.238
   * - 07:00
     - 0.355
     - 0.297
     - 0.275
     - 0.304
   * - 08:00
     - 0.477
     - 0.395
     - 0.349
     - 0.387
   * - 09:00
     - 0.487
     - 0.509
     - 0.48
     - 0.448
   * - 10:00
     - 0.473
     - 0.542
     - 0.532
     - 0.456
   * - 11:00
     - 0.45
     - 0.51
     - 0.567
     - 0.442
   * - 12:00
     - 0.448
     - 0.502
     - 0.576
     - 0.44
   * - 13:00
     - 0.458
     - 0.507
     - 0.591
     - 0.439
   * - 14:00
     - 0.436
     - 0.487
     - 0.552
     - 0.421
   * - 15:00
     - 0.431
     - 0.478
     - 0.539
     - 0.402
   * - 16:00
     - 0.468
     - 0.478
     - 0.563
     - 0.417
   * - 17:00
     - 0.554
     - 0.533
     - 0.629
     - 0.482
   * - 18:00
     - 0.65
     - 0.649
     - 0.698
     - 0.547
   * - 19:00
     - 0.723
     - 0.691
     - 0.763
     - 0.569
   * - 20:00
     - 0.709
     - 0.665
     - 0.757
     - 0.545
   * - 21:00
     - 0.661
     - 0.622
     - 0.685
     - 0.555
   * - 22:00
     - 0.593
     - 0.572
     - 0.606
     - 0.548
   * - 23:00
     - 0.496
     - 0.488
     - 0.497
     - 0.474
   * - 00:00
     - 0.36
     - 0.393
     - 0.358
     - 0.359


Metabolic activity
''''''''''''''''''''''''''''''''''''

Metabolic activity is calculated based on the parameters in the
database, which do not change over time (unlike energy consumption,
population and vehicle ownership).

The populace is assumed to emit more metabolic energy during waking
hours than during sleep, with a linear transition between these two
states based on the time people generally wake and sleep in each
country. A study area spanning national boundaries therefore shows
spatial variation in metabolic activity in the morning and evening if
the countries have different waking and sleeping hours in the LQF
database.

Recycling of temporal data
^^^^^^^^^^^^^^^^^^^^^^^^^^

The model calculates fluxes for any date provided there is temporal data
for the corresponding time of year. If daily temperatures and/or diurnal
cycles are not available for the date being modelled, a series of
lookups is performed on the available temporal data to find a suitable
match. This process accounts for changes in public holidays, leap years
and changing DST switch dates.

For diurnal cycle data, the lookup operates by building and then
reducing a shortlist of cycles that may be suitable:

#. Based on the modelled time step, cycles from a suitable year are
   added to the shortlist. A year is deemed suitable if it contains data
   covering the time of year being modelled

   -  If the modelled year is later than available data, the latest
      suitable year is used
   -  If the modelled year is earlier than the available data, the
      earliest suitable year is used

#. The modelled day of week is established (set to Sunday if a public
   holiday)
#. The lookup date is set as the same day of week, month and time of
   month as the modelled date, but in the year identified as suitable.

   -  This operation sometimes causes late December dates to become
      early January. Such dates are moved into the final week of
      December.

#. The daylight savings time (DST) state is identified for the lookup
   date, based on the time shift at noon.
#. Down-select the available cycles based on the DST state
   *(user-provided diurnal profile files only, when timezone of the
   modelled city is not the same as that in the profile file)*:

   -  If the cycles are not provided in the local time of the city being
      modelled, the search is narrowed to those cycles for
      periods/seasons matching this DST state
   -  If the cycles are provided in the local time of the city being
      modelled, all periods/seasons are available

#. Remove any cycles that do not contain the necessary day of week from
   the shortlist
#. The most recent cycle with respect to the lookup date is used

The same process is used to identify a relevant daily temperature,
except in this case a single value is looked up instead of a cycle and
each day of the year is its own season to improve resolution.

Further spatial disaggregation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is optional. It assigns transport, building and metabolism heat
fluxes to only those regions of that map with compatible land covers.
Since land cover fraction data are often available at high spatial
resolution, this increases the resolution of the model outputs beyond
the output areas that were specified initially.

Each model output area is divided into a number of “refined output
areas” (ROAs). The land cover fraction lists the proportion of each ROA
occupied by:

-  Water
-  Paved surfaces
-  Buildings
-  Soil
-  Deciduous Trees
-  Coniferous Trees
-  Grass

The GQF user interface requires two input files for this process.

-  **Land cover fractions**: Land cover fractions calculated using the
   `LandCoverReclassifier`
    in the pre-processing toolbox.
-  **Corresponding polygon grid**: The ESRI shapefile grid of polygons
   represented by the land cover fractions. This is a required input for
   the UMEP land cover classifier.

''Note that this feature may be very slow and memory limitations may
cause it to fail or produce very large output files. ''

The overall building, transport and metabolic Q\ :sub:`F` components in
an MOA are attributed to each ROA based on a set of weightings that
associate land cover classes with Q\ :sub:`F` components.

A fixed set of weightings determines the behaviour of this routine and
ensure the following principles are satisfied:

#. Transport heat flux only occurs on paved areas (roads)
#. Building heat flux only occurs where there are buildings
#. Metabolic energy reflects the distribution of people between indoor
   and outdoor environments

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - Land cover class
     -
     - Weightings (columns must sum to 1)
     -
   * -
     - Q\ :sub:`F,B`
     - Q\ :sub:`F,M`
     - Q\ :sub:`F,T`
   * - Building
     - 1
     - 0.8
     - 0
   * - Paved
     - 0
     - 0.05
     - 1
   * - Water
     - 0
     - 0.0
     - 0
   * - Soil
     - 0
     - 0.05
     - 0
   * - Grass
     - 0
     - 0.05
     - 0
   * - Deciduous Trees
     - 0
     - 0.0
     - 0
   * - Coniferous Trees
     - 0
     - 0.05
     - 0


Current limitations:

-  Building height not accounted for: same fraction of Q\ :sub:`F` would
   be assigned to a very tall building and short building if they
   occupied the same footprint, despite the former being likely to emit
   more heat per square metre of the surface it occupies
-  Land cover data: assumed to be consistent with the original input
   data. If non-zero building energy is calculated in an MOA that has a
   building land cover of zero, then this energy is lost.

Temperature response functions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Built-in response
^^^^^^^^^^^^^^^^^

LQF contains a database of country-specific parameters that link
temperature to building energy consumption via heating degree days (and
cooling degree days if air conditioning is assumed to be significant in
that country). This forms a temperature response function.

In the model, mean daily building energy consumption is estimated by
dividing the annual consumption by the number of days in a year. For
each modelled day, this figure is multiplied by the temperature response
function for that day. This allows the model to estimate seasonal and
day-to-day variations in energy consumption and therefore QF. `Lindberg
et al.
(2013) <http://www.sciencedirect.com/science/article/pii/S2212095513000059>`__
details the response function and how it varies from country to country.

User-defined response
^^^^^^^^^^^^^^^^^^^^^

An alternative temperature response function can be used to override the
built-in values. This uses 7 parameters, illustrated below:

.. figure:: /images/T_response.png

     ```to do```


#. Tc: Temperature above which air conditioning is used [°C]
#. Th: Temperature below which heating is used [°C]
#. Ac: Coefficient relating temperature above Tc to energy consumption
#. Ah: Coefficient relating temperature below Th to energy consumption
#. c: Constant that sets minimum value
#. Tmin: Temperature below which energy use from heating stops varying
   [°C]
#. Tmax: Temperature above which energy use from cooling stops varying
   [°C]

Despite the direction of the slopes, Ah and Ac are both positive
coefficients that act on the absolute difference between T and Th or Tc
(respectively).

To activate the custom response function, the parameters must be
specified in the parameters file.

Configuration data
---------------------

The LQFsoftware has two configuration files:

-  `Data sources file`_: Manages the various input
   data files and their associated metadata
-  `Parameters_file`_: Contains numerical values and
   assumptions used in model calculations.


Parameters file
~~~~~~~~~~~~~~~~~~~~~

The LQF parameters file contains public holidays and numeric values used
in calculations. The table below describes the entries in each
parameters file.

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Parameter name
     - Description
   * - **params: Model run parameters**
     -
   * - -  timezone

     - The time zone of the modelled area. Expressed in Continent/City format (e.g. Europe/London). `https://en.wikipedia.org/wiki/List\_of\_tz\_database\_time\_zones List of valid time zones. <https://en.wikipedia.org/wiki/List_of_tz_database_time_zones_List_of_valid_time_zones.>`__.
   * - -  use\_uk\_holidays

     - Set to 1 to use UK public holidays (calculated automatically) or 0 otherwise
   * - -  use\_custom\_holidays

     - Set to 1 to use a list of public holidays (specified separately) or 0 otherwise
   * - -  custom\_holidays

     - A list of custom public holidays in YYYY-mm-dd format.
   * - -  avgspeed

     - Mean speed (metres per hour) of traffic
   * - -  emissionfactors

     - Emissions factors in [W.m-2] for cars, motorcycles and freight vehicles
   * - -  balance\_point\_temperature

     - Outdoor air temperature below/above which the building energy is assumed to change as a result of active heading/cooling.
   * - -  balance\_point\_multfactor

     - Factor applied to the difference between air temperature and balance point temperature to estimate the building energy response
   * - -  QV\_multfactor

     - Assumed proportion of vehicle fleet in use per day
   * - -  sleep\_metab

     - Assumed metabolic heat emission per person [W] while resting (sleep)
   * - -  work\_metab

     - Assumed metabolic heat emission per person [W] while active (awake)
   * - **CustomTemperatureResponse**:
     - **Optional parameters for a custom `temperature response <#Temperature_response_functions>`__ function**

   * - -  Th

     - Daily mean Temperature below which heating is used (celsius)
   * - -  Tc

     - Daily mean Temperature above which artificial cooling is used (celsius)
   * - -  Ah

     - Coefficient relating temperature below Th to energy consumption
   * - -  Ac

     - Coefficient relating temperature above Tc to energy consumption
   * - -  c

     - Constant that sets minimum value of response function
   * - -  Tmax

     - Temperature above which energy use is constant with temperature
   * - -  Tmin

     - Temperature below which energy use is constant with temperature

Values for the land cover weightings discussed above are also included
in the parameters file.

Example parameters file (without user-defined temperature response)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A model configuration for the UK, with two more public holidays than are
ordinarily present.

::

    &params
       timezone = \ “Europe/London”
       use_uk_holidays = 1 
       use_custom_holidays = 1 
       custom_holidays = '2016-06-21', '2016-06-22' 
       avgspeed = 48000. 
       emissionfactors = 25.92, 13.16, 108.42 
       balance_point_temperature = 12.
       balance_point_multfactor = 0.7
       QV_multfactor = 0.8
       sleep_metab = 75  
       work_metab = 175  
    /
    &landCoverWeights
       ! For optional additional spatial disaggregation, triplets of weightings for land cover classes
       ! Values for [Building, Transport, Metabolism] respectively
       grass           = 0, 0, 0.025
       baresoil        = 0, 0, 0
       paved           = 0, 1, 0.10
       buildings       = 1, 0, 0.85
       water           = 0, 0, 0
       decidioustrees  = 0, 0, 0.025
       evergreentrees  = 0, 0, 0
    /

User-defined temperature response section
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To override the built-in temperature response function, the following
section must be added to the parameters file (arbitrary values are used
here as examples)

::

    &CustomTemperatureResponse
       Th = 10
       Tc = 20
       Ah = 0.1
       Ac = 0.2
       c = 0.5
       Tmax = 50
       Tmin = -10
    /


Data sources file
~~~~~~~~~~~~~~~~~~~~~

The data sources file manages the library of shapefiles and temporal
profile files used by the model. It is divided into a number of sections
(described below).

Output areas
^^^^^^^^^^^^

The shapefile that defines the model output areas to be used: all input
data are disaggregated into these spatial units, and the model results
are shown using them. In the simplest case, the same shapefile is used
for both outputAreas and Residential population (see below).

There are three entries:

.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Parameter
     - Description
   * - Shapefile
     - Location of the shapefile on the local machine
   * - epsgCode
     - EPSG code (numeric) of the shapefile coordinate reference system
   * - featureIds
     - Column that contains a unique identifier for each output area (optional: order of the output areas in the file is used if empty). This is used for cross-referencing and is shown in the model outputs.

An example:

::

    &outputAreas
      shapefile = 'C:\LQF\PopDens_2014.shp'
      epsgCode = 27700
      featureIds = 'LSOA11CD' 
      /

International database
^^^^^^^^^^^^^^^^^^^^^^

Nation-level population, vehicle registrations, energy consumption and
socio-economic data for multiple years are stored in a Spatialite
database file. The location of this file is specified in the data
sources file as follows:

::

    &database
       path = 'C:\LQF\InternationalDatabase.sqlite'
    /

Residential population shapefile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Entries for the 'residentialPop' section of the data sources file
(residential population data) example:
::

    &residentialPop
       shapefiles = 'C:\LQF\popOA2014.shp'
       startDates = '2014-01-01'
       epsgCodes = 27700
    /

**Note:** The population **must** appear under the attribute “Pop” in
the residential shapefile.

Note that a “startDate” and “epsgCode” must be specified for each
shapefile. Providing the incorrect EPSG code will result in incorrect or
zero heat fluxes being modelled because the mis-projected model areas
never overlap.

Temporal data: Metabolism, energy use and transportation temporal profiles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Air temperature (required)
''''''''''''''''''''''''''''''''''''

Daily mean temperature (in the local time zone of the location being
studied) is a required input. Data can be provided for multiple years
using a comma-separated list of files.

Energy consumption and traffic flow profiles (optional)
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

The LQF database contains default diurnal profiles for traffic and
building energy consumption, and this varies if the study area overlaps
countries with different profiles. These profiles are overridden if
user-specified data are supplied instead, and the user-specified values
are applied to the entire study area.

An example that provides all three temporal data sources is shown below,
and two years of data are provided for air temperature.

::

    &temporal
       ! Mean daily air temperature data
       dailyTemperature = 'C:\LQF\dailyT_2013.csv', 'C:\LQF\dailyT_2014.csv'
       ! Diurnal profiles
       ! Omit entries to use default LQF database values
       diurnEnergy = 'C:\LQF\buildingProfiles.csv'
       diurnTraffic = 'C:\LQF\transportProfiles.csv'
    /

Using multiple temporal profile files
''''''''''''''''''''''''''''''''''''''''''''''''''''''
As with shapefiles, multiple temporal profile files can be loaded into
the model to capture different periods of time. All of the data is
combined into a single file inside the model, provided that none of the
periods described within the files clash.

Example data sources file
^^^^^^^^^^^^^^^^^^^^^^^^^

A complete data sources file appears as follows. Note that two data
files are specified for the daily temperature data so that a longer time
series can be modelled.

::

      ! ### Model output polygons
      &outputAreas
         shapefile = 'C:\LQF\population.shp'
         epsgCode = 32631
         featureIds = 'ID' ! The attribute to use as a unique ID for each areas (optional; for cross-referencing)
      /
      ! ### Residential population data for the city being studied
      ! Must contain total population in each area under the attribute \ “Pop”
      &residentialPop
         shapefiles = 'C:\LQF\population.shp'
         startDates = '2014-01-01'
         epsgCodes = 32631
         featureIds = 'ID'
      /
      &database
         path = 'C:\LQF\InternationalDatabase.sqlite'
      /
      &temporal
         ! Air temperature each day for a year
         dailyTemperature = 'C:\LQF\temp_2013.csv', 'C:\LQF\temp_2014.csv'
         ! Provide file(s) for building energy consumption and/or traffic flow diurnal cycles
         ! Omit entries to use default LQF database values
         diurnEnergy = 'C:\LQF\buildingProfiles.csv'
         diurnTraffic = 'C:\LQF\transportProfiles.csv'
      /

Troubleshooting
-----------------------

Known issues
~~~~~~~~~~~~~~~~~~~~~~

Time zone problem
^^^^^^^^^^^^^^^^^

Sometimes, a valid time zone in the Parameters or temporal input files
will be rejected by the model, resulting in a “Time zone problem” error
message.

This is usually fixed by upgrading the Python time zone library. In
Windows:

#. Find Osgeo4w shell in Start > Programs
#. Right-click it and select “run as administrator”
#. Enter the following command:

pip install pytz --upgrade 

Restart QGIS and try again.

QGIS crashes and quits
^^^^^^^^^^^^^^^^^^^^^^

An unresolved bug causes QGIS 2.18.x to crash and quit immediately after
the “preparing input data using data sources” has finished. After
restarting QGIS, the model run can be resumed by

-  Using the same parameters and data sources files
-  Setting a new output folder
-  Rather than processing the input data again, selecting the prepared
   input data from the old output folder.
-  Run the model as normal

This allows the preparation step to be skipped, making use of the
results from last time round.

Appendix A: Converting a population raster to a vector shapefile using QGIS
-----------------------------------------------------------------------------

Global population datasets are generally available as raster files, but
LQF requires a set of population counts as vector polygons. This guide
explains how to convert a raster dataset to a set of polygons for use in
LQF. Examples are shown using a Greater London population count dataset
at 250m resolution.

#. Load the raster file into QGIS

.. figure:: /images/RasterConvert1.png

    ```to do```


#. Rename the layer to “Pop” (this saves time later)
#. Make sure the project coordinate reference system (CRS) is the same
   as for the raster. To change it, click the label and choose the
   correct CRS from the list:
.. figure:: /images/RasterConvert2.png

    ```to do```


#. Create a vector grid aligned to the raster:

   -  Vector -> Research Tools -> Vector Grid

      .. figure:: /images/RasterConvert3.png

          ```to do```

   -  This will show the Vector Grid dialog box:

      .. figure:: /images/RasterConvert4.png

          ```to do```


      -  In **Grid Extent**:

         -  Choose “Pop”
         -  Click *Align extends and resolution to the selected raster
            layer* (unless you want to choose the grid parameters
            manually to extract a subset of the raster)
         -  Click *Update extents from layer* to fill in the text boxes

            -  If this option is not available, you will need to get the
               resolution of the raster layer by inspecting its metadata
               (right click the layer > Properties > Metadata > Pixel
               size)

      -  In **Parameters**:

         -  Check *Output grid as polygons*
         -  Choose where to save the resulting shapefile containing the
            grid
         -  Check *Add results to canvas* so the grid can be used

#. The raster values must now be extracted from the raster layer into
   the vector grid. Use the “Add raster values to features” tool from
   **Processing** > **Toolbox** > **SAGA** > **Vector to raster**:

   .. figure:: /images/Saga1.png

        ```to do```

   .. figure:: /images/Saga2.png

        ```to do```

   -  In *Parameters*, choose:

      -  Shapes: The vector grid that you created
      -  Grids: Press “...” and select the “Pop” raster layer
      -  Interpolation: Nearest neighbour (selects the nearest raster
         data point)
      -  Result: The location of a new shapefile that contains the
         vector grid and the population in each cell

   -  Press “Run”. The resulting shapefile will be added to the layers.
      It contains a “Pop” column for the population
   -  Use this shapefile as the residential population in LQF (in the
      `Data sources file`_)

Appendix B: Gathering information about shapefiles for QF modelling
---------------------------------------------------------------------

LQF and GQF usually need two pieces of information from within a
shapefile. This section explains how to find that information:

#. The EPSG code, which defines the coordinate reference system. This is
   needed so the model can convert between positions and units of
   measurement.
#. Feature ID field: An attribute within the output areas file that
   contains a unique identifier for each output area. This allows the
   model to cross-reference between areas.

Firstly, open QGIS and load the griddedResidentialPopulation.shp file by
dragging it into the map area (canvas). An opaque grid should appear.

Finding the shapefile EPSG code
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the Layers panel, right-click “griddedResidentialPopulation” and
choose “Set project CRS from Layer”.

.. figure:: /images/300px-LQF_Tutorial_GetEPSG1.png

      ```to do```

The
project CRS code in the bottom right-hand corner of the QGIS window will
then change to match that of the output areas file. Use the numeric part
of this to fill in the EPSGcode: entry of the data sources file:

.. figure:: /images/GetEPSG2.png

    ```to do```

Finding the unique feature identifier
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Right-click the layer again, and choose “Open Attribute Table”. The
table that appears contains one row for every output area in the file,
and one attribute for each column.

.. figure:: /images/LQF_Tutorial_FindIdentifier.png
   :alt: LQF_Tutorial_FindIdentifier.png


   ```to do```

In this case, the column with a unique value for every output area is
called “ID”. Use this name in the DataSources file.
