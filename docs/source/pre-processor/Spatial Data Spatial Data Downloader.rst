.. _SpatialDataDownloader:

Spatial Data: Spatial Data Downloader
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* Developer：
.. list-table::
   :widths: 50 50
   :header-rows: 0

   * - Name
     - Institution

   * - Andy Gabey
     - Reading


* Introduction：
   - The Spatial Data Downloader downloads geo-datasets useful for UMEP applications. Only the necessary section of the data is downloaded, so that disk use and download time are minimised.

* Dialog box:
    .. figure:: /images/650px-Downloader.png
    
        Dialog for the Spatial Data Downloader plugin

* Category and available datasets:
    - Each category contains multiple datasets, which are revealed by clicking the category name. To download a dataset, select it from the list, specify the geographic extent and press “Download”

* Abstract：
    - Information about the selected dataset, including citation information.

* Bounding box：
    - The geographic extent of the region to download (maximum download size is 500x500 pixels in the case of raster data). The current QGIS canvas extent can also be used by clicking **Use canvas extent**

* Reproject to current project CRS：
    - The downloaded data is saved in its original CRS by default. This option reprojects the saved data to the project CRS and performs resampling, the resolution of which is controlled by the “Pixel resolution in CRS units” box.

* Get data：
    - Refreshes the catalogue of available datasets. This is also updated when QGIS starts.

* Update list:
    - Refreshes the catalogue of available datasets. This is also updated when QGIS starts.

* Close:
    - Closes the plugin.
