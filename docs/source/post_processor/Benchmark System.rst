.. _Benchmark:

Benchmark System
~~~~~~~~~~~~~~~~
* Contributor:
.. list-table::
   :widths: 50 50
   :header-rows: 1

   * - Name
     - Institution

   * - Ting Sun
     - Reading
   * - Sue Grimmond
     - Reading

*  Overview :
     -  **Note**: the current version runs in a command-line interface (CLI) driven by Python and the GUI-based version is under construction.
     -  The Benchmark System for SUEWS (BSS) can be used with SUEWS to assess the model performance between different configurations and model generations. BSS is written in Python and shipped with an example namelist and an MS Excel spreadsheet for header lookup between different SUEWS versions.

* Benchmark results:
    -  Two types of metrics are provided: :
          -  overall performance score: a score between 0 and 100 with larger score denoting better overall performance
          -  specific statistics: a range of statistics, including Mean absolute error (MAE), root mean square error (RMSE), standard deviation (Std), etc., to indicate detailed performance in specific variables.
    -  The users can use the overall performance score to get the performance overview of all configurations (Fig. 1a) and specific statistics to examine the performance details (Fig. 1b).
        .. figure:: /images/300px-BSS-result.png

            BSS results for (a) the overall performance and (b) a specific statistics (e.g., RMSE)

* Usage:
    -  To use BSS, in addition to the mandatory BSS files (i.e., Benchmark\_SUEWS.py, benchmark.nml and head-2016to2017.xlsx), the SUEWS output results are required to be placed in a separate folder (e.g., “input”) that contains the sub-folders of results produced by different configurations. A sample layout of the BSS test case refers to Fig. 2. It must be noted that the output files to be benchmarked should be of consistent temporal organisation (i.e., identical length and resolution) while the headers of different files are not necessarily to be identical as BSS will handle the header inconsistency automatically. Besides, two sub-folders, “base” and “ref”, which contain the baseline results to be tested against and reference results to be compared with, respectively, must exist otherwise the BSS will stop.   |
    
    -   When the SUEWS output files are prepared, the namelist (i.e., benchmark.nml) needs to be set for the benchmarking. The benchmark namelist is fairly self-explanatory and consists two sections, “file” and “benchmark”, to play with. One tip is about the variable list (i.e., var\_list): if one non-string value is set (e.g., 123, 3.2, etc.), all valid variables will be included in the benchmarking. Then the user can execute the Benchmark\_SUEWS.py script and a PDF file with benchmark results will be generated (e.g., benchmark.pdf in Fig. 2).
          .. figure:: /images/300px-BSS-file-layout.png


              Required file organisation by BSS.
* Namelist: benchmark.nml:
     -  The benchmark namelist is fairly self-explanatory and consists two sections, “file” and “benchmark”, to play with.
     -  One tip is about the variable list (i.e., var\_list): if one non-string value is set (e.g., 123, 3.2, etc.), all valid variables will be included in the benchmarking.
     -  A sample namelist is as follows:
        ::
          &file
            input_dir = 'input'
            output_pdf = 'benchmark'
          /
          &benchmark
            list_var='QN' 'QS' 'QE' 'QH'
            list_metric='MAE' 'MBE' 'RMSE'
            method_score=1 ! not used yet
          /
