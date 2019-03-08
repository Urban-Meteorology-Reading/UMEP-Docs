.. _Known_Issues:




Known Issues
------------

-  QGIS (27/September/2017) **had** an issue using gdal which causes
   QGIS to create a minidump when the software is closed. This issue has
   now been fixed (issue
   #\ `13061 <https://hub.qgis.org/issues/13061>`__). Other issues found
   should be reported to our
   `repository <https://bitbucket.org/fredrik_ucg/umep/issues>`__.
-  UMEP plugin for QGIS3 is not compatible with matplotlib versions 3.0.0. Use
   instead 2.3.3 (25/October/2018).
-  Mac users might have issue pointing at non-existing directories. Work
   around is to manually create directories before starting any
   UMEP-process.
-  Only use standard English alpha-numeric characters (e.g. no space, å,
   % etc.)
-  Issues has been reported using .sdat rasters. GeoTiff are
   recommended.
