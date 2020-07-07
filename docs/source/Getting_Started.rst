.. _Getting_Started:


Getting Started
===============

Recommended Installation of QGIS on Windows
-------------------------------------------

#. Visit `QGIS <http://www.qgis.org>`__ and go to the download page. Preferably, choose the `OSGEO4W Network Installer (64-bit) <http://download.osgeo.org/osgeo4w/osgeo4w-setup-x86_64.exe>`__, start the installation and choose *installation (64-bit) For Advanced Users*.
#. **To install the latest version (3.x)**, start the installation and choose *Express Desktop Install*.

Visit `www.qgis.org <http://www.qgis.org>`__ for installation on other operating systems.

Installing the UMEP-plugin
--------------------------
#. Go to: *Plugins -> Manage and Install Plugins...* in QGIS Desktop.

#. Under the *All*-tab, Search for **UMEP**.

#. Click on **UMEP** and then click **Install Plugin**. We recommend you to click **OK** to the popup question below. That will save you troubles later on. The python libraries that will be installed (if not present on your system) can be found `here <https://github.com/sunt05/SuPy/blob/d48f58d8f35e852acd4e205ca4b0a3c9adcdebf2/src/setup.py#L40-L58>`__.

  .. figure:: /images/Installsupy.jpg
     :alt:  None
     :align: center

     When installing UMEP related Python packages can be installed by clicking **OK**. Packages can also be installed later (see below).

As from Spring 2020 parts of UMEP is also available as a `processing plugin <UMEPforProcessing>`. Install the same way but search for **UMEP for processing**. Also remember to tick in **show also experimental plugins** under the *Settings*-tab.

Test `datasets <https://urban-meteorology-reading.github.io/>`__ and `tutorials <https://umep-docs.readthedocs.io/projects/tutorial/en/latest/index.html>`__ are available to try some of the tools out. Since QGIS is a multi-platform software system it works on other platforms as well. UMEP is constanlty under development so there may be missing documentation and instability. Please report any issues to the `issue tracker <https://github.com/UMEP-dev/UMEP/issues>`__. Also, have a look in `FAQ <FAQ>` for further installation tips and issues.

Updating the UMEP-plugin
------------------------
#. Go to: *Plugins -> Manage and Install Plugins...* in QGIS Desktop.

#. Search for **UMEP**.

#. Click on **UMEP**. If a new version is available, this will be stated here. If so, click **Upgrade Plugin**.


.. _Python_Libraries:

Adding missing Python libraries and other OSGeo functionalities
---------------------------------------------------------------

Some of the plugins in the UMEP tool requires some Python libraries such as
**scipy** and **pandas** that
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
              1. (**Try this first**) Run the *osgeo4w-setup-x86_64.exe* (or *osgeo4w-setup-x86_32.exe* depending on your system) executable. This can be found using the Windows search bar. Select *Advanced Install* -> *Install from Internet*. The next four pages will give options to select the *Installation Directory*, *Local Package Directory*, *Connection Type* and *Download Site*. Alter these as required. In most cases the default entries will be fine. When you come up to the *Select Packages* page, search for the requied package (e.g. pandas) and click on *Skip* until you see a version number of pandas (see image below). Finish the installation.

                .. figure::  /images/Pandas.png

                   Example of installation of pandas using the *Installation (64-bit) For Advanced Users*

              2. **pip** is a command to install python packages but pip cannot be used directly from a common command line window (**cmd.exe**). However, if you installed QGIS according to the recommendations in `Getting started <Getting_Started>` you should have a **OSGeo4W shell** installed where you can use pip to add desired Python libraries. **OSGeo4W shell** is found in the Windows start menu. To use it with QGIS3, type **py3_env** the first thing you do after you have open **OSGeo4W shell**.

                You need to run the shell as an administrator of your PC. To do this, right-click on **OSGeo4W shell** and choose *run as administrator*. To install e.g. pandas, write the command below in the command window that has appeared:
                ::
                  py3_env
                  python3 -m pip install pandas

                If nececcary, you can also install other versions of python libraries using **pip**
                ::
                   pip uninstall netCDF4
                   pip install netCDF4==1.2.9

                to upgade a library:
                ::
                  pip install netCDF4 --upgrade

        #. Mac OS X
            - Follow the instructions for Linux. **Note**: this approach is tested to be working under Mac OS X 10.11.5.
        #. Other Platforms
            - Other platforms require the packages to be installed to the QGIS Python path, which differs depending on operating system.
              Or refer to `startup.py <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/intro.html#the-startup-py-file>`__
              to modify start up file of QGIS by including the paths to **pandas** and **scipy**. An example of startup.py may look like
              ::
                 import sys
                 sys.path.insert(1,'/usr/local/lib/python3.7/site-packages')


Installing development release (could be unstable)
--------------------------------------------------
#. Download UMEP from the `repository <https://github.com/UMEP-dev/UMEP>`__, as a ZIP-file. The main branch at the moment is **SuPy-QGIS3**.
#. If you have an installed version of UMEP in your QGIS, uninstall it by going to “Plugins -> Manage and Install Plugins -> Installed -> UMEP” and click **Uninstall plugin**.
#. Go to “Plugins -> Manage and Install Plugins -> Install from zip”.
#. Restart QGIS. The UMEP plugin should be visible in the QGIS toolbar. If not, go to “Plugins -> Manage and Install Plugins -> All” and search for UMEP. Make sure that you also tick in the box *Show also experimental plugins* in the “Settings”-tab.
