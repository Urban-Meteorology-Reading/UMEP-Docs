.. _UMEPforProcessing:


UMEP for Processing
===================

**UMEP for Processing** ports the UMEP tools to the `QGIS processing framework <https://docs.qgis.org/3.10/en/docs/user_manual/processing/intro.html>`__, which is a geoprocessing environment that can be used to call native and third-party algorithms from QGIS, making your spatial analysis tasks more productive and easy to accomplish. You can for example call the UMEP tools directly as function in a Python script of include them in the Graphical Modeler in QIS.

UMEP for processing (Experimental and not complete) is available from *Plugins -> Manage and Install Plugins...* in the menu bar in QGIS. Remember to tick in **show also experimental plugins** under the **Settings**-tab.

More tools, info and tutorials is under contruction. The code is available on our Github page, under the `umep-processing <https://github.com/UMEP-dev/UMEP/tree/umep-processing>`__ branch.


.. _UMEPforProcessingRoadMap:

Road map for UMEP for Processing
--------------------------------

Below you can see which tools that have been migrated to UMEP fro processing and what tools that will not be migrated. Please report any issues to our `repository <https://github.com/UMEP-dev/UMEP>`__. 

MetdataProcessor - Will not be migrated

ShadowGenerator - READY

SkyViewFactorCalculator - READY

ImageMorphParam - READY

ImageMorphParmsPoint - READY

LandCoverFractionGrid - READY

LandCoverFractionPoint - READY

LandCoverReclassifier - READY

WallHeight - READY

TreeGenerator - NOT READY

FootprintModel - NOT READY

LCZ_converter - NOT READY

UMEP_Data_Download  - NOT READY

DSMGenerator  - NOT Ready

ERA5 DownloadData  - READY

GreaterQF  - NOT READY

ExtremeFinder - NOT READY

LQF - NOT READY

SEBE - NOT READY

SuewsSimple - Will not be migrated

SUEWSPrepare - NOT READY

SUEWSConverter - Will not be migrated

SUEWS - READY

SOLWEIG - NOT READY

BenchMarking  - Will not be migrated

SEBEVisual - Will not be migrated

SolweigAnalyzer - Will not be migrated

SUEWSAnalyzer - Parts will not be migrated

