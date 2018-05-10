.. _Getting_Started:

Getting Started
==================
* **Overview**：

         + UMEP is developed as a plugin for `QGIS <http://www.qgis.org>`__. Two versions are available:
               -  *Long term release* - This version is recommended for most users.
               -  *Development release* - This version is for testing. Could be unstable.
         + For a more detailed description including how to install QGIS on a Windows PC (see below) or watch this instruction `video <https://www.youtube.com/watch?v=ZEw_DVl772Q>`__. You can find more introductory videos on how to use UMEP on our `YouTube-channel <https://www.youtube.com/channel/UCTPkXncD3ghb5ZTdZe_u7gA>`__.
         + UMEP has been developed using Python 2.7.x and QGIS 2.x in a Windows environment. Since QGIS is a multi-platform software system it works on other platforms as well. UMEP is still under development so there may be missing documentation and instability. Please report any issues to the `code repository <https://bitbucket.org/fredrik_ucg/umep>`__. Also, have a look in `FAQ <http://urban-climate.net/umep/UMEP_Manual#FAQ>`__ for further installation tips and issues.

* **Recommended Installation Steps of QGIS on Windows**：

                    -  Visit `QGIS <http://www.qgis.org>`__ and go to the download page. Preferably, choose the `**OSGEO4W Network Installer (64-bit)** <http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe>`__, start the installation and choose *installation (64-bit) For Advanced Users*
                    -  Start the installation and choose *Express Desktop Install*. This includes a number of OSGEO-software as well as a separate python installation.

* **Long-term release** - Download and installation of the UMEP-plugin from within QGIS：

          #. Start **QGIS**

          #. Go to: *Plugins -> Manage and Install Plugins...*

          #. Search for **UMEP**

          #. Click **Install Plugin** (or *Upgrade* if already have an older version installed from before).

* **Development release** - Download and installation of the UMEP-plugin from the UMEP code repository (unstable)

          #. If you have an installed version of UMEP in your QGIS, uninstall it by going to “Plugins -> Manage and Install Plugins -> Installed -> UMEP” and click **Uninstall plugin**
          #. To download UMEP from the repository click this `link <https://bitbucket.org/fredrik_ucg/umep/downloads>`__ and download repository
          #. Close QGIS if open
          #. Extract the downloaded zip archive into the folder **C:\\Users\\\\.qgis2\\python\\plugins**. If the folder **plugins** does not exist, install any plugin using *Plugins -> Manage and Install Plugins* and the folder should appear.
          #. Rename the extracted folder to **UMEP**
          #. Start QGIS. The UMEP plugin should be visible in the QGIS toolbar. If not, go to “Plugins -> Manage and Install Plugins -> All” and search for UMEP. Make sure that you also tick in the box *Show also experimental plugins* in the “Settings”-tab.
      + **NOTE**: Remove old versions of UMEP from the plugin directory before you update.


* **Test dataset** ：
    +  Can be used try some of the tools out (`testdata\_UMEP.zip <https://bitbucket.org/fredrik_ucg/umep/downloads/testdata_UMEP.zip>`__).


Adding missing Python libraries and other OSGeo functionalities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Some of the plugins in the UMEP tool, for example The WATCH data plugin,
requires some Python libraries such as **pandas** and **scipy** that
might not been included when you installed QGIS. If so, it is necessary
to install them to make this plugin work. Below are instructions on how
to this for different operation systems. The same procedures can also be
used to obtain other tools and functionalities from the OSGeo
repository. **Note**: In order for scipy to work you will also need to
make sure *pillow* is installed.


* **Operating System and Installation instructions**：

        #. Linux
            - Linux comes with its own Python installation which QGIS makes use of. This makes it possible to directly use **pip** (an installation tool of Python libraries) to add missing libraries. Simply open a terminal window and type *sudo pip install pandas* if you want to install this library. In order to install pip open a terminal and type: *sudo easy\_install pip*. You might need to restart QGIS to get it to work.
            - Or refer to `startup.py <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/intro.html#the-startup-py-file>`__ to modify start up file of QGIS by including the paths to **pandas** and **scipy**. An example of startup.py may look like:
              ::
                 import sys
                 sys.path.insert(1,'/usr/local/lib/python2.7/site-packages')

        #. Windows
            -  There are two options available:
              1. As Windows has no Python installation included, QGIS make use of a separate Python installation added when QGIS was installed on your PC.

                This results in that pip cannot be used directly. However, if you installed QGIS according to the recommendations in `Getting started <http://urban-climate.net/umep/UMEP_Manual#Getting_Started>`__ you should have a **OSGeo4W shell** installed where you can use pip to add desired Python libraries. **OSGeo4W shell** is found in the Windows start menu.

                You need to run as an administrator of your PC. To do this, right-click on **OSGeo4W shell** and choose *run as administrator*. In the command window that appear, write:
                ::
                  pip install pandas

              2. Installation of pandas Restart the *installation (64-bit) For Advanced Users* (see Getting started) and choose *Advanced Install*. When you come up to Select Packages search for pandas and click on *Skip* until you see a version number of pandas (see left picture). Finish the installation.

                **This method can also be used to include other missing libraries such as gdal etc.**

                \ **PLEASE NOTICE!**\

                Due to a recent update of **netCDF4** library (1.3.0), the **netCDF4** library has a version conflict related to the **numpy** version currently used in QGIS 2.18.x. This results in that some plugins in UMEP will fail, e.g. LQf.
                We have submitted an issue regarding this to the QGIS community. Meanwhile, we recommend UMEP users to downgrade the netCDF4 library to **1.2.9**. This is easiest done by opening the **OSGeo4W shell** and run the two following commands:
                ::
                   pip uninstall netCDF4
                   pip install netCDF4==1.2.9
                .. figure::  /images/Pandas.png
                **Installation of pandas**


        #. Mac OS X
          - Follow the instructions for Linux. ***Note***: this approach is tested to be working under Mac OS X 10.11.5.
        4. Other platforms require the packages to be installed to the QGIS Python path, which differs depending on operating system. Or refer to `startup.py <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/intro.html#the-startup-py-file>`__
          to modify start up file of QGIS by including the paths to **pandas** and
          **scipy**. An example of startup.py may look like:
          ::
             import sys
             sys.path.insert(1,'/usr/local/lib/python2.7/site-packages')
