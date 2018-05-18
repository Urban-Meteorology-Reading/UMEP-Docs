Contributing with python code to the UMEP plugin in QGIS
--------------------------------------------------------

Here, instructions and recommendations on how to make your own plugin to
go with the UMEP plugin will be described as well as tips and tricks on
how to make use of the GIS capabilities included in QGIS to go with your
plugin.

Gary Sherman (creator of QGIS) has produced a number of useful tools for
developers that can be used to make your own contribution to the
software. Below, a number of tool are listed that come very handy when
you want to create your own plugin. There is also a number of resources
online that is very useful. One is the `PyQGIS Developer
Cookbook <http://docs.qgis.org/testing/en/docs/pyqgis_developer_cookbook/>`__
available from the QGIS webpage and another is a book written by Gary
Sherman called The `PyQGIS Programmer's
Guide <http://locatepress.com/ppg>`__.

#. Start off by creating a plugin using the **PluginBuilder** in QGIS.
   This is a plugin that sets up all necessary files and folders for
   your plugin.
#. Another useful plugin is the **PluginReloader** which makes it
   possible to reload a plugin in QGIS without restarting the software.
#. pb\_tool is another useful program to use for installing your plugin
   in the QGIS plugin folder as well as cleaning etc.

Please use the python libraries that comes with the QGIS installation as
much as possible without including external libraries when developing
your plugin. All libraries are not included when a common installation
of QGIS is installed. Go to our `Getting
started <http://urban-climate.net/umep/UMEP_Manual#UMEP:_Getting_Started>`__
section for further instructions.

External Python libraries currently included in the UMEP plugin
(Utilities folder):

-  f90nml - for reading and writing of fortran namelists
-  Pysolar - for calculation of Sun positions

To use the f90nml library located in the Utilities folder:

::

  from ..Utilities import f90nml

The **pandas** library is not install by default so a simple install
pandas cannot be used use instead a try statement:

::

  try:
      import pandas
  except Exception, e:
      QMessageBox.critical(None, 'Error', 'The WATCH data download/extract feature requires the pandas package '
                             'to be installed. Please consult the FAQ in the manual for further information')
      return

The same goes for **matplotlib** and other libraries that you are
uncertain of.

SUEWS wrapper
~~~~~~~~~~~~~~~

The main file of the python wrapper for the SUEWS model is called
SUEWSwrapper.py. To change version of SUEWS when running the wrapper,
simple go in to SUEWSwrapper.py and activate the line which is calling
the appropriate wrapper (e.g. SUEWSwrapper\_v2016a) and comment out
other versions.

In SUEWS v2017b - this is no longer used/needed

f2py
~~~~~~~~~~~~~~~

A possibility to make use of fortran subroutines in python. See
`here <http://docs.scipy.org/doc/numpy-dev/f2py/>`__ for documetation.

#. When developing the fortran code for compiling with f2py kind=1d0
   will not work for function parameters to be passed in from python.
   Should use KIND=8.

Setting up Windows machine for running f2py
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please note that the steps below contain some links that over time could
change, however, the basics should remain the same. This has been tested
and established for an Intel 64-bit machine running NT operating system.
This is still to be tested on other versions of Windows operating
system. If you carry out on both OS, please add to the list below or
report to team.

The process can also be applied to a 32-bit machine, but the choice of
python2.7 and set up for MinGW-w64 will be different. This has not been
tested, and perhaps shouldn’t be encouraged if SUEWS is being developed
and tested on/for 64-bit architecture.

Before starting any of the required steps it is recommended that any
version of Python, mingw, and Cygwin be removed from the machine if
possible. If you already have Python 2.7 and MinGW installed, or have
followed the procedure below then go to the instructions on developing
fortran-python interface.

System Setup
^^^^^^^^^^^^

#. Download Python 2.7.XX : download from:
   `here <http://www.python.org/downloads>`__ and install to directory
   C:\\Python27<!--



#. Add to PATH environment variable:

    C:\\Python27

    C:\\Python27\\libs

    C:\\Python\\Scripts


#. Add to C\_INCLUDE\_PATH environment variable:


    C:\\Python27\\include

    C:\\Python27\\libs


**Note:** The *C:\\Python27\\Scripts* directory is required for use of
pip in subsequent steps.

#. Install latest NumPY package to get latest f2py

    (i) Download numpy-1.11.0rc1+mkl-cp27-cp27m-win\_amd64.whl from
    `here <http://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy>`__

    (ii) Open command prompt and change directory to where numpy wheel is
    installed (e.g. Downloads folder). Run the following command:

    ::

      Pip install numpy-1.11.0rc1+mkl-cp27-cp27m-win_amd64.whl

    (iii) Check the directories for **numpy** and
    **numpy-1.11.0rc1.dist-info** are under
    **C:\\Python27\\Lib\\site-packages**. Dates and times of directory
    should indicate these are new from wheel.


#. Download Mingw-w64 from
   `here <https://sourceforge.net/projects/mingw_w64>`__


   **Note:** This is suitable for 64 and 32 bit architecture.



#. Run mingw-w64-install.exe (found in directory to which you have
   downloaded it to).

    (i) In the install procedure set:


    **Version:** 5.3.0 (or what ever is latest)

    **Architecture:** x86\_64 (for 64 bit machine)

    **Threads:** posix

    **Exception:** dwarf

    **Build revision:** 0



    (ii) Set the destination folder to: **C:\\mingw-w64\_x86** when
    prompted.


#. Add to environment variable:



    (i) **C\_INCLUDE\_PATH: C:\\mingw-w64\_x86\\mingw64\\include**

    (ii) **PATH: C:\\mingw-w64\_x86\\mingw64\\bin**


#. This step is required to create/replace the import library found
   under directory **C:\\Python27\\libs**. The import library is
   **libpython27.a**.

    (i) Download the pexports binary **pexports-0.47-mingw32-bin.tar.xz**
    from
    `here <http://www.sourceforge.net/projects/mingw/files/MinGW/Extension/pexports/pexports-0.47/>`__.

    **Note:** pexports-0.47 could change for subsequent versions.


    (ii) Unpack the tar file and put pexports.exe in **C:\\Python27\\libs**.


    #. Open a command prompt and run the following command:

    ::

       pexports C:\Windows\System32\python27.dll > USERDIR\python27.def


    **Note:** *USERDIR* is the user directory you put the file in. As it is
    an intermediary step and a temporary file, the user directory you use
    shouldn’t matter, however, don’t try to put it in Windows\\System32
    directory, or any other directory in the system Path.

#. Create the import library **libpython27.a** for helping the linker of
   MinGW link to the correct python DLL.


   (i) Open Command Prompt and change directory to where *python27.def* was
   created in step 8 (i.e.USERDIR*).

   (ii) Run command:

   ::

     dlltool –D python27.dll –d python.def –l libpython27.a

   (iii) Move resulting *libpython27.a* into **C:\\Python27\\libs** ,
   replacing any existing version of this file in the directory

Making Fortran-Python Interface ‘dll’ (.pyd file) with F2PY
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  This is shown using a makefile (named *Makefile*) that is called from
   the command line as follows:

::

    mingw32-make  –f  Makefile

**Note:** This should be called from within the directory that the
Makefile and source code is in.

-  Basic Makefile:

::

     CC = gnu95
     CCO= x86_64-w64-mingw32-gfortran
     FFLAGS = -fPIC
     TARGET = INTENDED_NAME_OF_PYD
     MODULES = nameOfModules.o

     main:  NAMEOFMAINPROGRAMFILE.f95  $(MODULES)
      f2py.py –c –-fcompiler=$(CC) –-compiler=mingw32 –m $(TARGET) NAMEOFMAINPROGRAMFILE.f95 $(MODULES)

     $(MODULES): nameOfModules.f95
     $(CCO) –c  $(FFLAGS)  nameOfModules.f95

     cleanall:
        -del $(MODULES)


**Note:** A .pyd file should have been created on the completion of
compilation from command called in step 1.


-  Create a directory to store all created .pyd files in (e.g.
   C:\\PythonPYD) and add to PATH environment variable.


This ensures the .pyd files are picked up and used by python scripts.

Distributing f2py Modules for Windows
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Note:** all the .dll files (including those used to make python
library from MinGW) need to be packaged up so that a machine without MinGW can use the
developed python libraries.

The .dll files to include are: NEED TO LIST THEM

Importing and using in Python
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Import the module into python script in the same way you would import
   any other module:


    - If your module is called *SolweigShadow*, for example, then *import
    SolweigShadow as SS* will enable you to access the functions of the
    module by *SS.functionName()*.

    **Note:** The parentheses are needed regardless of whether the function
    has parameter inputs/outputs.


#. To see what functions are available for the imported module, use the
   command
   ::

     print hw.__doc__

Upcoming Developments
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table::
   :widths: 25 25 25 25
   :header-rows: 1

   * - U/S
     - Topic
     - Status
     - Lead
   * - SUEWS
     - Snow
     - Completed
     - Univ Helsinki
   * - SUEWS
     - Convective boundary layer development
     - Completed
     - Göteborg Univ
   * - SUEWS/SOLWEIG
     - Mean radiant temperature model
     - Active
     - Göteborg Univ
   * - SUEWS
     - Storage Heat flux - ESTM
     - Completed
     - Göteborg Univ /Reading
   * - SUEWS
     - Storage Heat flux - AnOHM
     - Active
     - Reading/Tsinghua
   * - SUEWS
     - Anthropogenic Heat fluxes
     - Actve
     - Reading
   * - Multi
     - Benchmark
     - Active
     - Reading
   * - Wind
     - Pedestrian wind speed
     - Active
     - Göteborg Univ/Reading
   * - Multi
     - Downscaling data \*download WATCH
     - Active
     - Lingbo Xue (Reading)/TS
   * - Multi
     - Downscaling data \*precip mass check
     - Active
     - TK/ LX (LJ/TS)
   * - Multi
     - Downscaling data \*precip intensity
     - Active
     - AG/ LX
   * - SUEWS/SOLWEIG
     - Radiation coupling
     - Active
     - Göteborg Univ/Reading

Benchmarking system
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Benchmark <http://urban-climate.net/umep/Benchmark>`__

Coding Guidelines
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

SUEWS
^^^^^^^^^^^^^^^^^^^^^^^^^^

If you are interested in contributing to the code please contact Sue
Grimmond.

#. Code written in Fortran – currently Fortran 95
#. Variables

   -  Names should be defined at least in one place in the code –
      ideally when defined
   -  Implicit None should be used in all subroutines
   -  Variable name should include units. e.g. Temp\_C, Temp\_K
   -  Output variable attributes should be provided in the TYPE
      structure defined in the ctrl_output module as follows:

       ::

           : TYPE varAttr
           : CHARACTER(len = 15) :: header ! short name in headers
           : CHARACTER(len = 12) :: unit   ! unit
           : CHARACTER(len = 14) :: fmt    ! output format
           : CHARACTER(len = 50) :: longNm ! long name for detailed description
           : CHARACTER(len = 1)  :: aggreg ! aggregation method
           : CHARACTER(len = 10) :: group  ! group: datetime, default, ESTM, Snow, etc.
           : INTEGER             :: level  ! output priority level: 0 for highest (defualt output)
           : END TYPE varAttr

#. Code should be written generally
#. Data set for testing should be provided
#. Demonstration that the model performance has improved when new code
   has been added or that any deterioration is warranted.
#. Additional requirements for modelling need to be indicated in the
   manual
#. All code should be commented in the program (with initials of who
   made the changes – name specified somewhere and institution)
#. The references used in the code and in the equations will be
   collected to a webpage
#. Current developments that are being actively worked on

How to setup your development environment on Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

gfortran with NetBeans
^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Go to Cygwin and install 64-bit. You need to make sure that you
   install gfortran, g++, gdb, make and gcc. I am not really sure what
   is needed so I tend to install too many packages rather that too few.
   Install in c:\\cygwin64
#. Go to your Environment Variables in advanced system settings in
   windows and include

   C:\\cygwin64\\bin;C:\\cygwin64\\usr\\bin;C:\\cygwin64\\usr\\local\\bin;C:\\cygwin64\\lib;C:\\cygwin64\\usr\\lib
   in your Path.

#. Install NetBeans from www.netbeans.org. You only need to download the
   C/C++ version.
#. If you don’t have the correct Java, follow the link presented to you
   and install correct version.
#. Copy your code to a folder of your choice.
#. Create a new project (C/C++ from Existing Source) and use you folder
   as the project folder. Keep all other settings.
#. You are ready to work.

NOTE: Another nice thing to do is to use gfortran from your cluster on
your windows PC. Do the following:

-  In Netbeans, go to Tools>Options>C/C++ and click Edit next to
   localhost. Click Add… and write metcl2. Just keep on clicking until
   you need to give your username and password for the cluster.
-  Now you should be able to run GNU on the cluster from your windows
   PC.

Python and PyCharm (Not so good alternative)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Install python 2.7.X, 64 bit from python.org (Windows x86-64 MSI
   installer). Install with default settings.
#. Visit JetBrain, Pycharm website and obtain a student account (go to
   **Discounted and Complimentary Licenses**,
   https://www.jetbrains.com/pycharm/buy/). Click on **For Students and
   Teachers**, go to bottom of the page and click **Apply Now**. Choose
   either a student or a teacher status. You will get an email where you
   activate your license.
#. Create a folder which you can use as a project folder. Copy the
   python code (\*.py) from the suews repository and put it the folder.
   If you don’t have access to the repository talk to Fredrik Lindberg.
#. Download PyCharm professional
   (https://www.jetbrains.com/pycharm/download/) and install.
#. Start PyCharm and activate license using your JetBrains account.
#. Create a new project (Pure python) and choose the created folder (3)
   as your project folder and use your python installation as
   interpreter. Click ok in the next message box.
#. Go to File>Settings >Project Interpreter. Add a new package by
   clicking the green plus sign. Search for numpy and install package.
   If you get errors, you probably need correct version of Visual
   studio. There is an address of a website where you can download it in
   the error message when you tried to install numpy.
#. Also install matplotlib (used for plotting)
#. Run mainfileLondon.py to do stuff.

 

Python and PyCharm (good alternative)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Go to qgis.org and click on download. Choose the installation for
   advanced users (64-bit). Choose the **advanced desktop installation**
   and make sure that **qgis-ltr** is included. Keep other default
   settings. This give you a python installation with everything you
   need (pretty much). IF you are missing python libraries after the
   installation, you can restart the installation file and add more
   components.
#. If you haven’t installed PyCharm, follow set 2 through 5 above.
#. Create a .bat-file (e.g. PyCharmWithQgis.bat) with the following
   content (put it in your folder created earlier and edit it so that
   the paths on line 1 and 5 is correct):
    ::

      SET OSGEO4W_ROOT=C:\OSGeo4W64
      SET QGISNAME=qgis
      SET QGIS=%OSGEO4W_ROOT%\apps\%QGISNAME%
      SET QGIS_PREFIX_PATH=%QGIS%
      SET PYCHARM= “C:\Program   Files   (x86)\JetBrains\PyCharm   2017.3.5\bin\pycharm.exe
      CALL %OSGEO4W_ROOT%\bin\o4w_env.bat
      SET PATH=%PATH%;%QGIS%\bin
      SET PYTHONPATH=%QGIS%\python;%PYTHONPATH%
      start  “PyCharm   aware   of   QGIS”\  /B %PYCHARM% %*

#. Run the bat-file.

How to make standalone application using py2exe (this is not used, see below)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. In PyCharm, add the pip package (if not already there). See bullet
   point 6. Above.7.
#. Go to http://www.lfd.uci.edu/~gohlke/pythonlibs/ and download the
   appropriate py2exe package (.whl).
#. Open a command prompt and go to the folder where you download the
   py2exe package and write:
   ::
     pip name_of_whl_file

#. Create a file called setup.py in your working directory with the
   following code:
      ::

          from distutils.core import setup
          import py2exe

      ::

            setup(console=['Suews_wrapper_v2015a.py'])

#. From a command prompt (can use terminal in PyCharm) write:

python setup.py install

#. Then write:

     ::

         python setup.py py2exe

#. All files and folders needed are now created in a subfolder call
   dist. You also have to add the SUEWS executable and all files needed
   to run the model.

How to make standalone application using Pyinstaller (use this)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Add the pip package (see above)
#. You need to add the path to where pip.exe is located (usually
   C:\\Python27\\Scripts\\). If you don’t know how to add a path in your
   environment settings you can temporarily add one in a command prompt
   by writing:

      ::

           path %PATH%;C:\Folder_where_pipexecutable_is_located

#. In the same command prompt, write:

      ::

           pip install pyinstaller

#. Locate yourself where you have your script and write:

      ::

          pyinstaller suews_wrapper_v3.py

SUEWS Prepare Developer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is for advanced users regarding SUEWS Prepare plugin in UMEP. The
information in should help with translating the plugin, adding new tabs
or adding new variables.

* most important files for making changes to the plugin
    - excel documents SUEWS\_init.xlsx, SUEWS\_SiteLibrary.xls and SUEWS\_SiteSelect.xlsx.
* files are located
    - as a part of the plugin in the folder named “Input” (by default in C:\\Users\\your\_username\\.qgis2\\python\\plugins\\SUEWSPrepare\\Input).
* SUEWS Prepare uses these files
    - for example to generate the amount of site library tabs and the contents of those tabs.
* Take care
    - any changes made to these documents will be lost if they are replaced (e.g. reinstalling or updating the plugin). This can be prevented by making backups of the excel documents before reinstalling or updating.
* SUEWS\_init.xlsx
    - This file handles the amount of site library tabs in the plugin, the name of these tabs and their connection to other excel sheets and text documents. Each sheet represents one tab.
* SUEWS\_SiteLibrary.xls
    - This file contains all the different information connected to different site. Each excel sheet is connected to a different kind of information like vegetation and water data and each line in a sheet represents a different area or site. This information is used to determine what kind of information and variable will be present in a widget of a site library tab.


      .. figure:: images/Figure14.png


          Empty widget not connected to any sheet from the SUEWS_SiteLibrary document.

SUEWS\_SiteSelect.xlsx
^^^^^^^^^^^^^^^^^^^^^^^^^

* A detailed look at the SUEWS_init document
    - This file contains an example of one line of output from the plugin. It is used by the plugin to check the order of the outputs. It can be considered the least important and useful for developers.  
* Modifying the plugin
    - How to work with the excel documents to make changes to existing information inside the plugin such as titles. This could be required for translation or to fix spelling errors.
* **Changes available through SUEWS\_init.xlsx**
    - The SUEWS\_init determines the number of site library tabs as well as the number of widgets in these tabs and where the widgets will fetch their content. The document contains a number of sheets and every sheet represents one site library tab. The names of the sheets will determine the title of the site library tab. The first one is an example of how the layout of a working sheet should look.

    .. figure:: /images/Figure15.png

        Example of the layout of a sheet in the SUEWS_init document.

    - Each row of a sheet represents a new widget. Every column of the row is used to determine the specific characteristics of the widget.

.. list-table::
   :widths: 5 25
   :header-rows: 0

   * - 1
     - The content of a widget such as variables are determined by a sheet from the document SUEWS\_SiteLibrary (See `#XLS <#XLS>`__). The first column of a row in a sheet in SUEWS\_init makes the connection between a widget and a sheet in SUEWS\_SiteLibrary. This means that the content of the first column will be the name of a sheet in SUEWS\_SiteLibrary.
   * - 2
     - As well as being connected to a sheet in SUEWS\_SiteLibrary each tab needs to be connected to a text document. This text document will basically be a copy of the site library sheet and will be part of the plugin output. All available text documents are located in the folder named “Output” in the plugin directory and will have the same name as the sheets in SUEWS\_SiteLibrary. The contents of the second column will be the full name of a text document including the file extension, for example “SUEWS\_Veg.txt”.
   * - 3
     - determines the title of the widget’s variable box.
   * - 4
     - optional and determines if there is an identification code for the widget. The identification code is an integer number is used when multiple widgets share a site library sheet but shouldn’t share the same site entries. If an identification code is added the widget will only fetch site entries that match the code. If no identification code is need the column is left blank.
   * - 5
     - determines if there is a default site entry that should be selected in the widget’s drop down menu when the plugin is initiated. If the site code of a site entry (see `#XLS <#XLS>`__) is added to the fifth column this site entry will be automatically selected in the widget on plugin start up.
   * - 6
     - When the plugin generates an output each widget will provide the selected site code in the widget as part of the output. The sixth column is the index of the site code in the plugin output. It should not be changed without careful consideration as there is a risk of the site code overwriting other information in the output if it is.

.. figure:: /images/Figure16.png
    :align: right

     Red outline illustrates the title for the widget variable box.      




* Change the variables in the variable box of a widget
    - The content of a widget is decided by what sheet in the document SUEWS\_SiteLibrary.xls it is connected to. This connection is created by the information in the first column of a sheet in SUEWS\_init. To make changes edit the text in the first column to match the name of the sheet you want to fetch information from. Example: Let’s say for the purposes of this example that we want the content of the tab named “Paved” to have the same content of the tab named “Evergreen”. To do this we must change the connection in the paved sheet of SUEWS\_init to match that of the evergreen sheet. In the evergreen sheet we can see it’s connected to a sheet in SUEWS\_SiteLibrary called SUEWS\_Veg. If we change the text of the first column in the paved sheet to match this, the content of the tab will change to the same as the evergreen tab. ```PICTURE? this needs attention```

.. list-table::
   :widths: 5 25
   :header-rows: 0

   * - 2
     - is like the first a kind of connection but instead of a sheet it’s to a text document. The text file is close to a copy of the sheet a tab is connected to. If the sheet connection is changed the text file connection should be changed as well. Example: If we did the changes to the paved tab in the example above. In the current state of the paved sheet any changes (for example adding a new site) made would write to the wrong text file. Therefore we also need to change the second column to match the correct text file. In this case to “SUEWS\_Veg.txt”

- **Change the title of the variable box in the widget**

.. list-table::
   :widths: 5 25
   :header-rows: 0

   * - 3
     - title of the variable box in the widget. “Variable box” is referring to the box on the right hand side of the widget that contains the variables from the site library. If the title needs to be changed simply edit the text in the third column of the correct sheet and the new title of the box will match that. Example: Following the above examples, the title “Building surface characteristics” no longer matches the content of the variable box in the paved tab. Replace the text in the third column to “Vegetation surface characteristics” and our title will now make more sense.   ```PICTURE? this needs attention```

* Change the default parameters for a widget
    - fourth and fifth columns are optional information and decide if there are any default parameters for a widget. The number in the fourth column decides if there is an identification code for the tab. This identification code is used to exclude entries from the site library. Many tabs might link to the same site library sheet and if there is an identification code only the entries that match the code will be shown in the widget. If there is a number in the fifth column the tab will try to match this number against the site codes (not to be confused with the identification code). The side codes are the codes that fill out the drop down box in the widget marked “code” and each code represent one site library entry. If there exist a default site code for a tab this code will be selected in the drop down menu on the plugin start up. Example: Let’s keep making changes to the paved sheet. Right now the identification code for the sheet is “1” and the default site code is “661”. If we change the identification code (fourth column) to “4” a different set of site entries will be available for selection in the widget. One of the site codes that are now available is “662”. By changing the content of the fifth tab to “662” this will now be the default site code for the widget.   ```PICTURE? this needs attention```
    * Change the order of the widget site code in the final output of the plugin
    - A widget’s contribution to the final output of the plugin will be the selected site code in the widget. This code will be placed somewhere on a predetermined place in a long list of variables. The sixth column in a SUEWS\_init sheet represents this position in the final output. To change a widget’s output order edit the number in the sixth column. Take care to make sure changing the position doesn’t overwrite any other information. The order of the final output is also closely tied to the document SUEWS\_SiteSelect, see more [[#XLSX].
* Editing a tab name
    - The name of the tabs in the SUEWS Prepare main window correspond to the names of the sheets in the excel document SUEWS\_init. To edit a tab name simply change the name of the sheet.
    - Example: After all the changes made to the paved sheet in SUEWS\_init the name “paved” as a description of the tab no longer fit. By renaming the sheet to “vegetation” the tab will have a more fitting name.  ```this needs attention PICTURE?```
* Changes available through SUEWS_SiteLibrary.xls
    - What can be made through the SUEWS\_SiteLibrary.xls.
    - The SUEWS\_SiteLibrary document is what defines the variables inside a tab. This document defines the titles and tooltips for the variables as well as the values for the variables on different sites.

        .. figure:: /images/Figure17.png


            Different rows of a site library sheet highlighted with different color. For the variable title row and the site entry rows the different purposes of the columns have been illustrated.

* Variable index
    - first row of a site library sheet is an index of the variables in the sheet.
* Variable and metadata titles
    - second row contains the titles of the variables. The first cell is always the title “Code”. After all the variable titles follows a blank cell. The cells that follows will be titles for metadata, it is also possible that there is no metadata for the sheet. The row always end with the titles “Photo”, “LC\_previous” and “LC\_code” in that order.
* Variable tooltips
    - third row contains tooltips or longer descriptions of the variable titles.
* Site entries
    - A site entry represents one complete set of values for all the variables in the sheet. One row represents one site entry. The first cell of a site entry always contains the site code. This code is used to differentiate between different site entries and needs to be a unique integer number for the sheet. The following cells contain values for different variables until an exclamation mark marks the end of variables. If there are any metadata descriptions these will be in the cells following the exclamation mark. The last three cells are in order: a photo url if there is one otherwise the cell is left blank, a blank cell and lastly the identification code if there is one (otherwise the cell is left blank). The two last rows: The two last rows of the sheet contains a single “  -9” in the first cell. These rows are used by the plugin to signify the end of the data in the sheet and nothing below these rows will be read.
* Change the title of a variable
    - To change the title of a variable, first navigate to the correct sheet in SUEWS\_SiteLibrary. The titles of all variables are decided by the text in the second row. Replace the text in a column to change the name of a single variable or for example translation purposes replace every word in the second row with its translation.
* Change the tooltip of a variable
    - The tooltip of a variable is a longer description than the title that shows up when the user hovers over the variable text box.
        .. figure:: /images/Figure18.png

            Tooltip of a variable.
    - The third row of a SUEWS\_SiteLibrary sheet defines the tooltip of a variable. To changes it, replace the text for the relevant column in the third row.

* Changes available through SUEWS\_SiteSelect.xlsx
    - The document SUEWS\_SiteSelect.xlsx is mainly connected to the final output of the plugin. Most developers won’t need to make any changes to it. Developers mainly concerned with the layout of the SUEWS Prepare plugin will not need to be concerned about SUEWS\_SiteSelect.

* Change the order of the final output
    - The second row of the sheet SUEWS\_SiteSelect contains text strings that are used by the plugin to identify a variables place in the final output of the plugin. Changing the order of the strings in the second row will similarly affect the final output.

Adding to the plugin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
How to make additions to the plugin (e.g. adding new tabs). Earlier information will be useful when adding to the plugin. i.e. read earlier sections before reading this one.

* Adding a new tab to the plugin
    - As discussed (`#XLSX <#XLSX>`__) the excel document SUEWS\_init.xlsx is closely tied to how the plugin generates tabs. The plugin will generate tabs according to the number of sheets in this excel document and according to the information in the sheets. A single sheet represents one new tab. Every row in a sheet represents a widget that will be added to the tab. Every column in a sheet contains certain information that decides the specifics for a widget such as what variables will be added. The first sheet of the excel document is an example sheet that can be used as a quick reference for the content of the columns. For a more detailed description see `#XLSX <#XLSX>`__.
* To add a new tab to the plugin:
      #. Create a new sheet in the SUEWS\_init document. The order of the sheets will match the order of the tabs in the plugin. Do not place the sheet first in the excel document as this is used as a placeholder for the example sheet. The name of the sheet will become the title of the tab.
      #. Add the name of a sheet from the SUEWS\_SiteLibrary document to the first column. This will be what decides the content of the first widget in the tab. See `#ADD <#ADD>`__ if there is a need to create a new sheet for the tab.
      #. Add the name of a text file that will receive the output of the widget to the second column. In most cases the text file should have the same name as the sheet from step two. Make sure to add the file extension, for example .txt, to the second column as well.
      #. Add a title for the widget in the third column. This title should describe what the variables in the widget represent, for example “Paved surface characteristics”.   *
      #. The content of the fourth column is optional. This column contains a code that can be used if multiple tabs share a sheet from SUEWS\_SiteLibrary. The code is used to identify what site entries belong to which tab and widget. (See `#XLS <#XLS>`__) Leave the column empty if no identification code is needed.
      #. The content of the fifth column is optional. This column can be used if there is a site entry in the sheet from step two that should be selected in the widget’s drop down menu by default. Enter the site code of a site entry in the fifth column to make it the default. Note that the site code is not the same as an identification code (See `#XLS <#XLS>`__). Leave the column empty if there is no default site.
      #. The sixth column represents the index of the widget output in the order of the plugins final output. The widget output will be the site code selected in the drop down menu. Make sure that the index doesn’t overwrite an already existing output. The easiest way to make sure of this is to check the document SUEWS\_SiteSelect for the index of the last variable and use the index after the last variable.
      #. To add more widgets to the tab, follow the instructions from step 2 and forward again on the following rows of the sheet.


* <div id="ADD" Adding a new set of site variables to the plugin</div>
      - As discussed in `#XLS <#XLS>`__ the variables of a site (and consequently the variables that appear in a widget connected to this site) are generated from the excel document SUEWS\_SiteLibrary. One sheet represents the variables of a type of site and can be connected to multiple widgets and tabs. A new site sheet must fulfil certain conditions. The first row of the sheet should be an index of the variables in the sheet that ranges from one to the amount of variables. The second row should       contain the titles for the variables and the first column should always be “Code”. Furthermore the second row should always end with the titles “Photo”, “LC\_previous” and “LC\_code” in that order. The third row should contain longer tooltips or descriptions of the variables. The rows following the third row should each represent one site entry. Lastly the sheet should end with two rows that just contains “  -9” in the first column. For a more detailed description see `#XLS <#XLS>`__.

      - There are two options when adding site entries; it can be done manually directly in the sheet or through the plugin when the sheet has been connected to a widget. (See Section 6.1 and 3.3.2)

      - When adding a site entry manually certain conditions must be followed:

          -  The first entry should be the site code for the entry. This needs to be an integer unique for the sheet.
          -  The column following the last variable needs to contain an exclamation mark designating the end of the variables.
          -  If there are metadata titles for the sheet the information for these should be entered in the columns following the exclamation mark. Metadata is optional for all site entries.
          -  For the last three mandatory titles; the “Photo” column can contain a url link to a picture representing the site entry. The “LC\_previous” column can be left blank. The “LC\_code” column can contain an identification code if this is needed for the site entry.

      - Each new sheet needs a matching text document located in the “Output” directory of the plugin. This text document needs to mimic most of the excel sheet. Instead of columns separating the variables the text document should use tab indents and each line in the text document represents a row in the sheet. The first line of the text document should be an index of the variables. The second line should be the variable titles. The text document should not contain the variable tooltips therefore       the site entries should start on the third line of the text document as opposed to the fourth row of the excel sheet. Any site entries added manually to the excel sheet needs to be manually entered to the text document as well. The two last lines of the text document should just contain a single “  -9”. To add a new site library sheet use the methodology above and follow these steps:

        #. Create a new sheet in the excel document SUEWS\_SiteLibrary.
        #. If you know how many variables the sheet will contain start numbering the first row of the sheet from 1 in the first column to the amount of variables in the last column. Otherwise fill in this row when all the variable titles have been entered. The numbering should end where an exclamation mark would be entered for a site entry.
        #. Add the variable titles in the second row. Start with “Code” in the first column. Leave a column blank where the exclamation mark for a site entry would be entered. If there are any metadata descriptors relevant for the site add the title for these after the blank column. Examples of this could be “City”, “Area” or “Description”. After adding any metadata descriptors add “Photo”, “LC\_previous” and “LC\_code” in the last three columns of the row in that order.
        #. Add the tooltips of the variables to the columns in the third row. These should be longer descriptions of what the variable represents.
        #. OPTIONAL: Add any site entries manually to the sheet. Use a new row for each site entry. The other option is to use the plugin to add all the entries. One benefit of using the plugin is that the site entries will be added automatically to the text document as well as the excel sheet.
        #. Add “  -9” to the first column of the two last rows of the excel sheet.
        #. Create a text document in the “Output” directory of the plugin. Name it after the excel sheet if possible.
        #. Make a copy of the variable index in the first row of the sheet as the first line of the text document. Use tab indents as a replacement for columns.
        #. Make a copy of the variable titles in the first row of the sheet as the second line of the text document. Use tab indents as a replacement for columns.
        #. Copy any manually added site entries in the sheet to the text document. Each site entry is a new line in the text document. Use tab indents as a replacement for columns.
        #. End the text document with two lines, both only containing a single “  -9”.
