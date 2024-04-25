=============
Installation
=============

Python
======

It is suggested to use a virtual environment or docker image to install INTEGRATE in Python
For example, in Ubuntu you can use the following commands to create a virtual environment and install INTEGRATE:

:: 
    
        sudo apt-get install python3-venv
        python3 -m venv integrate
        source integrate/bin/activate
        

The following packages are required using INTEGRATE with Python:

::

        pip install numpy scipy matplotlib jupyterlab h5py tqdm 
        pip install integrate

or 

::
    
            cd /path/to/integrate_module
            pip install .   

In addtiton you will need to install one of the EM forward codes described below. 

CURRENTLY ONLY GA-AEM is supported.

MATLAB
======


The following packages are required using INTEGRATE with MATLAB:

- `sippi <https://github.com/cultpenguin/sippi>`_
- `mgstat <https://github.com/cultpenguin/mgstat>`_
- `sippi-abc <https://github.com/cultpenguin/sippi-abc>`_

In addtiton you will need to install one of the EM forward codes described below. 

CURRENTLY ONLY GA-AEM is supported.

..
    Julia
    =====



FORWARD MODELING
================


GA-AEM [GA-AEM]
---------------
GA-AEM can be downloaded from [https://github.com/GeoscienceAustralia/ga-aem].

**On Windows:** 

You need to add `path_to_ga-aem/third_party/fftw3.2.2.dlls/64bit/` to the Windows path `$PATH` under
environment variables. 

Then add `path_to_ga-aem/matlab/gatdaem1d_functions/` and `path_to_ga-aem/matlab/bin/x64/` to the Matlab path
::

    addpath path_to_ga-aem/matlab/gatdaem1d_functions/
    addpath path_to_ga-aem//matlab/bin/x64/


**On Linux/OSX:**

MEX files need to be compiled after downlading the source. Edit the `run_make.sh` to adapt to your local system before compiling using:
::

    sudo apt-get install build-essential
    sudo apt-get install libfftw3-dev
    sudo apt-get install libopenmpi-dev

    cd path_to_ga-aem/makefiles
    ./run_make.sh

Then add `path_to_ga-aem/matlab/gatdaem1d_functions/` and `path_to_ga-aem/matlab/bin/linux/` to the Matlab path

::

    addpath path_to_ga-aem/matlab/gatdaem1d_functions/
    addpath path_to_ga-aem/matlab/bin/linux/




SimPEG [Python only]
--------------------
[SimPEG]_ can be installed using pip:

::

    pip install simpeg


AarhusInv [Windows only]
------------------------
To use AarhusInv [AarhusInv]_ it must be installed and the path to the executable must be added to the path variable.
In addition a valid license must be associated with the installation.



