.. _UMEPforProcessing:


UMEP for Processing
===================

**UMEP for Processing** ports the UMEP tools to the `QGIS processing framework <https://docs.qgis.org/3.10/en/docs/user_manual/processing/intro.html>`__, which is a geoprocessing environment that can be used to call native and third-party algorithms from QGIS, making your spatial analysis tasks more productive and easy to accomplish. You can for example call the UMEP tools directly as functions in a Python script or include them in the Graphical Modeler in QIS.

UMEP for processing (Experimental and not complete) is available from *Plugins -> Manage and Install Plugins...* in the menu bar in QGIS. Remember to tick in **show also experimental plugins** under the **Settings**-tab.

More tools, info and tutorials is under contruction. The code is available on our Github page, under the `umep-processing <https://github.com/UMEP-dev/UMEP/tree/umep-processing>`__ branch.


Accessing algorithms in a stand-alone Python script 
---------------------------------------------------

By make use of **processing for UMEP** there are possibilities to export UMEP-tools to a standalone Python script. One easy way to do this is to run a certaion tool from the *Processing Toolbox* and copy the syntax from the log-tab or from the History log in the QGIS Processing toolbox.

Below you see a commmand example running the *Wall Height and Aspect*-tool copied from the History log after running the tool through the toolbox:
::
  processing.run("umep:Urban Geometry: Wall Height and Aspect", 
     {'INPUT':'C:/temp/DSM.tif',
     'ASPECT_BOOL':True,
     'INPUT_LIMIT':3,
     'OUTPUT_HEIGHT':'C:/temp/height.tif',
     'OUTPUT_ASPECT':'C:/temp/aspect.tif'}
  )

To access third party processing plugins (such as UMEP) in a stand-alone Python script, use the following lines of code (example for Windows users):
::
  from qgis.core import QgsApplication
  import sys

  # Initiating a QGIS application
  qgishome = 'C:/OSGeo4W64/apps/qgis/'
  QgsApplication.setPrefixPath(qgishome, True)
  app = QgsApplication([], False)
  app.initQgis()

  # import third party processing plugins
  sys.path.append(r'C:\Users\ **your_username** \AppData\Roaming\QGIS\QGIS3\profiles\default\python\plugins')
  from processing_umep.processing_umep_provider import ProcessingUMEPProvider
  umep_provider = ProcessingUMEPProvider()
  QgsApplication.processingRegistry().addProvider(umep_provider)



.. _UMEPforProcessingRoadMap:

Road map for UMEP for Processing
--------------------------------

Below you can see which tools that have been migrated to UMEP fro processing and what tools that will not be migrated. Please report any issues to our `repository <https://github.com/UMEP-dev/UMEP>`__. 

.. list-table:: 
   :widths: 50 50
   :header-rows: 1

   * - MetdataProcessor
     - Will not be migrated
   * - ShadowGenerator
     - READY
   * - SkyViewFactorCalculator
     - READY
   * - ImageMorphParam
     - READY
   * - ImageMorphParmsPoint
     - READY
   * - LandCoverFractionGrid
     - READY
   * - LandCoverFractionPoint
     - READY
   * - LandCoverReclassifier
     - READY
   * - WallHeight
     - READY
   * - TreeGenerator
     - NOT READY
   * - FootprintModel
     - NOT READY
   * - LCZ_converter
     - NOT READY
   * - WallHeight
     - READY
   * - UMEP_Data_Download 
     - NOT READY
   * - DSMGenerator
     - NOT READY
   * - GreaterQF
     - NOT READY
   * - ERA5 DownloadData
     - READY
   * - UMEP_Data_Download 
     - NOT READY
   * - ExtremeFinder
     - NOT READY
   * - LQF
     - NOT READY
   * - SEBE
     - READY
   * - SuewsSimple 
     - Will not be migrated
   * - SUEWSPrepare
     - NOT READY
   * - SUEWSConverter
     - Will not be migrated
   * - SUEWS
     - READY
   * - SOLWEIG 
     - READY
   * - BenchMarking
     - Will not be migrated
   * - SEBEVisual
     - Will not be migrated
   * - SolweigAnalyzer
     - Parts will be migrated
   * - SUEWSAnalyzer
     - Parts will be migrated



