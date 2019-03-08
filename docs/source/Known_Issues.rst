.. _Known_Issues:

Known Issues
------------
-  (25/October/2018) The UMEP plugin for QGIS3 is not compatible with matplotlib versions 3.0.0. Use
   instead 2.3.3. Follow the instruction at `link <Python_Libraries>` and use the commands:
   ::
     pip uninstall matplotlib
     pip install matplotlib==2.2.3
-  Mac users might have issue pointing at non-existing directories. Work
   around is to manually create directories before starting any
   UMEP-process.
-  Only use standard English alpha-numeric characters (e.g. no space, å,
   % etc.)
-  Issues has been reported using .sdat rasters. GeoTiff are
   recommended.
