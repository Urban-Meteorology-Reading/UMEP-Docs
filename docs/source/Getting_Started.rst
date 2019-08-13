.. _Getting_Started:


Getting Started
===============

Recommended Installation Steps of QGIS on Windows
-------------------------------------------------

.. note:: As UMEP-version for QGIS2 is depreciated since February 2019, the new long-term release version of QGIS is 3.x.

#. Visit `QGIS <http://www.qgis.org>`__ and go to the download page. Preferably, choose the `OSGEO4W Network Installer (64-bit) <http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe>`__, start the installation and choose *installation (64-bit) For Advanced Users*.
#. **To install the latest version (3.x)**, start the installation and choose *Express Desktop Install*.
#. **To install the** `LTR <Abbreviations>`, start the installation and choose *Advanced Install*. Click through to *Select Packages* and select *qgis-ltr-full*.

Visit `www.qgis.org <http://www.qgis.org>`__ for installation on other operating systems.

Installing the UMEP-plugin
--------------------------

Long-term release (Recommended)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Start **QGIS**

#. Go to: *Plugins -> Manage and Install Plugins...*

#. Search for **UMEP**

#. Click **Install Plugin** (or **Upgrade** if already have an older version installed from before).


Development release (could be unstable)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. If you have an installed version of UMEP in your QGIS, uninstall it by going to “Plugins -> Manage and Install Plugins -> Installed -> UMEP” and click **Uninstall plugin**.
#. To download UMEP from the repository click this `link <https://bitbucket.org/fredrik_ucg/umep/downloads>`__ and download repository.
#. Close QGIS if open.
#. Extract the downloaded zip archive into the folder **C:\\Users\\\\.qgis2\\python\\plugins**. If the folder **plugins** does not exist, install any plugin using *Plugins -> Manage and Install Plugins* and the folder should appear.
#. Rename the extracted folder to **UMEP**.
#. Start QGIS. The UMEP plugin should be visible in the QGIS toolbar. If not, go to “Plugins -> Manage and Install Plugins -> All” and search for UMEP. Make sure that you also tick in the box *Show also experimental plugins* in the “Settings”-tab.

Test `datasets <https://bitbucket.org/fredrik_ucg/umep/downloads/testdata_UMEP.zip>`__ and `tutorials <http://umep-docs.readthedocs.io/en/latest/tutorial/docs/source/index.html>`__ are available to try some of the tools out.

Since QGIS is a multi-platform software system it works on other platforms as well. UMEP is constanlty under development so there may be missing documentation and instability. Please report any issues to the `code repository <https://bitbucket.org/fredrik_ucg/umep>`__. Also, have a look in `FAQ <FAQ>` for further installation tips and issues.


.. _Python_Libraries:

Adding missing Python libraries and other OSGeo functionalities
---------------------------------------------------------------

Some of the plugins in the UMEP tool, for example The WATCH data plugin,
requires some Python libraries such as **scipy** and **pandas** that
might not been included when you installed QGIS. If so, it is necessary
to install them to make this plugin work. Below are instructions on how
to this for different operation systems. The same procedures can also be
used to obtain other tools and functionalities from the OSGeo
repository.

* **Operating System and Installation instructions**：

        #. Linux
            - Linux comes with its own Python installation which QGIS makes use of. This makes it possible to directly use **pip** (an installation tool of Python libraries) to add missing libraries. Simply open a terminal window and type *sudo pip install pandas* if you want to install this library. In order to install pip open a terminal and type: *sudo easy\_install pip*. You might need to restart QGIS to get it to work.
            - Or refer to `startup.py <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/intro.html#the-startup-py-file>`__ to modify start up file of QGIS by including the paths to **pandas** and **scipy**. An example of startup.py may look like:
              ::
                 import sys
                 sys.path.insert(1,'/usr/local/lib/python3.7/site-packages')

        #. Windows
            -  As Windows has no Python installation included, QGIS make use of a separate Python installation added when QGIS was installed on your PC. There are two options available.
              1. (**Try this first**) Installation of e.g. pandas Restart the *installation (64-bit) For Advanced Users* (see Getting started) and choose *Advanced Install*. When you come up to Select Packages search for pandas and click on *Skip* until you see a version number of pandas (see left picture). Finish the installation.
                   
                .. figure::  /images/Pandas.png

                   Example of installation of pandas using the *Installation (64-bit) For Advanced Users*
                
              2. **pip** is a command to install python packages but pip cannot be used directly from a common command line window (**cmd.exe**). However, if you installed QGIS according to the recommendations in `Getting started <Getting_Started>` you should have a **OSGeo4W shell** installed where you can use pip to add desired Python libraries. **OSGeo4W shell** is found in the Windows start menu. To use it with QGIS3, type **py3_env** the first thing you do after you have open **OSGeo4W shell**.

                You need to run the shell as an administrator of your PC. To do this, right-click on **OSGeo4W shell** and choose *run as administrator*. To install e.g. pandas, write the command below in the command window that has appeared:
                ::
                  py3_env
                  pip install pandas
                  
                If nececcary, you can also install other versions of python libraries using **pip**  
                ::
                   pip uninstall netCDF4
                   pip install netCDF4==1.2.9
                  
        #. Mac OS X
            - Follow the instructions for Linux. ***Note***: this approach is tested to be working under Mac OS X 10.11.5.
        #. Other Platforms
            - Other platforms require the packages to be installed to the QGIS Python path, which differs depending on operating system. 
              Or refer to `startup.py <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/intro.html#the-startup-py-file>`__
              to modify start up file of QGIS by including the paths to **pandas** and **scipy**. An example of startup.py may look like
              ::
                 import sys
                 sys.path.insert(1,'/usr/local/lib/python3.7/site-packages')
