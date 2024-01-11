=============
Data format
=============

The HDF5_ file format is used as a container for all data in INTEGRATE. 
Each HDF5 file can contain multiple data sets (typically arranged in matrix format) with associated attributes that describe the data. `HDF View`_ is usefull to inspect the content of HDF5 files.

.. _HDF View: https://www.hdfgroup.org/downloads/hdfview/
.. _HDf5: https://www.hdfgroup.org/solutions/hdf5/


The following HDF files are used for any INTEGRATE project 

**DATA.h5** : Stores observed data, and its associated geometry.

**PRIOR.h5**: Stores realizations of the prior model, and corresponding forward response

**FORWARD.h5**: Stores information need to solved the forward, problem, and/or needed to describe the observed data in DATA.h5

**POST.h5**: stores index of posterior realizations, as well as posterior statistics 


DATA.h5
=======
DATA.h5 contains observed data, and its associated geometry. 
The observed data can be of many types, such as TEM data and well-log data
  
  ``Ns``: Number of soundings
  
  ``Nd``: Number of data points per sounding
  
  ``Nclass``: Number of classes

.. list-table:: Data and features om DATA.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset
     - Format
     - Feature
     - Mandatory
     - Description
   * - /D1/noise_model
     - [string]
     - *
     - *
     - A string describing the noise model used for the data. Here ``'gaussian'``
   * - /D1/d_obs
     - [Ns,Nd]
     - 
     - *
     - Observed data (#1)
   * - /D1/d_std
     - [Ns,Nd]
     - 
     - *
     - Standard deviation of observed data (db/dT). Is the size is [1,Nd], the same ``d_std`` is used for all data.
   * - /D1/Ct
     - [Nd,Nd]
     - 
     - 
     - Correlated noise matrix. ``Ct`` is the same for all data
   * - /D1/Ct
     - [Ns,Nd,Nd]
     - 
     - 
     - Correlated noise matrix; each data observation has its own correlated noise matrix 
   * - /D2/noise_model
     - [string]
     - *
     - *
     - A string describing the noise model used for the data. Here ``'class_probability'``
   * - /D2/d_obs
     - [Nc,Nclass,Nm]
     - 
     - 
     - Observed data (class probabilities)
   * - /D2/i_group
     - [Nd]
     - 
     - 
     - 
   * - /D2/i_use
     - [Nd,Nd]
     - 
     - 
     - Correlated noise matrix. ``Ct`` is the same for all data
   * - /UTMX
     - [Nd,1]
     - 
     - *
     - X - location of data points

   * - /UTMY
     - [Nd,1]
     - 
     - *
     - Y - location of data points    
   * - /ELEVATION
     - [Nd,1]
     - 
     - *
     - Elevation at data points    
   * - /LINE
     - [Nd,1]
     - 
     - *
     - Linenumber at data points    
   * - /gatetimes
     - [Ndata,1]
     - 
     - 
     - Gate times (in seconds) for each data point
   * - /i_lm
     - [Nlm,1]
     - 
     - 
     - Index (rel to /gatetimes) of Nlm gates for the low moment. 
   * - /i_hm
     - [Nhm,1]
     - 
     - 
     - Index (rel to /gatetimes) of Nhm gates for the high moment. 



PRIOR 
=====

PRIOR.h5 contains ``N`` realizations of a prior model (represented as potentially multiple types of model parameters, such as resistivity, lithology, grainsize,....), and corresponding data (consisting of potentially multiple types of data, such as tTEM, SkyTEM, WellData,..)

``N``: Number of realizations of the prior model

``Nm1``: Number of model parameters of type 1

``Nm2``: Number of model parameters of type 2

``NmX``: Number of model parameters of type X


.. list-table:: PRIOR model realizations in PRIOR.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset
     - Format
     - Feature
     - Mandatory
     - Description
   * - /M1
     - [N,Nm1]
     - 
     - *
     - N realizations of model parameter 1, 
       each consisting of Nm1 model parameters
   * - /M1/z
     - [nm]
     - *
     - *
     - Array of z values (top of layer) for M1
   * - /M1/is_discrete
     - [nm]
     - *
     - *
     - [0/1] described whether /M1 is a discrete or continuous parameter
   * - /M1/class_id
     - [1,n_class]
     - *
     - 
     - A list of  ``n_class`` class id; only when case /M1/is_discrete=1.
   * - /M1/class_name
     - [1,n_class]
     - *
     - 
     - A list of ``n_class`` strings describing each class; only when case /M1/is_discrete=1.
   * - /M1/clim
     - [1,2]
     - *
     - 
     - Min and maximum value for colorbar
   * - /M1/cmap
     - [3,nlev]
     - *
     - 
     - Colormap with ``nlev`` levels.
   * - /M2
     -  [N,Nm2]
     - 
     - 
     - N realizations of model parameter 2, 
       each consisting of Nm2 model parameters
   * - /Mx
     -  [N,NmX]
     - 
     - 
     - N realizations of model parameter X, 
       each consisting of NmX model parameters



.. list-table:: prior data realizations in PRIOR.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset
     - Format
     - Feature
     - Mandatory
     - Description
   * - /D1
     - [N,Nd1]
     - 
     - *
     - N realizations of data number 1, 
       each consisting of ``Nd`` model parameters
   * - /D1/f5_forward
     - [string]
     - *
     - 
     - HDF file describing the forward model used to compute prior data.
   * - /D1/with_noise
     - [1]
     - *
     - 
     - Indicates whether noise was added to the data[1] or not[0].
   * - /D2
     -  [N,Nd2]
     - 
     - 
     - N realizations of data number 2, 
       each consisting of ``Nd2`` model parameters
     

``/D1`` is only mandatory when PRIOR.h5 is used for inversion

All the mandatory features specified for ``/M1`` are also mandatory for other features, i.e.  ``/M1``,  ``/M2``, ... . 


f_forward_h5 [string]: Defines the name of the HDF5 file that contains information need to solved the forward problem...



FORWARD.h5
==========
The FORWARD.h5 needs to hold' as much information as needed to define the use fo a specific forward model.

The attribute ``/method`` refer to a specific choice of forward method.


.. list-table:: posterior data realizations in PRIOR.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset
     - Format
     - Feature
     - Mandatory
     - Description
   * - /method
     - [string]
     - *
     - 
     - Defines the type of forward model def:'TDEM'.
   * - /type
     - [string]
     - *
     - 
     - Define the algorithm used to solve the forward model. def:'GA-AEM'.
     

``/method`` can, for example, be ``tdem`` for Time Domain EM (YThe default in INTEGRATRE)

TDEM: Time domain EM, method='tdem'.
------------------------------------

``/method='TDEM'`` make use of time-domain EM forward modeling. 
The following three types of forward models will (eventally) be available:


``/type='GA-AEM'`` [DEFAULT].
[GA-AEM]_. Avilable for both Linux and Windows, Matlab and Python.


``/type='AarhusInv'``.
[AarhusInv]_. Windows only.
Not yet implemented


``/type='SimPEG'``.
[SimPEG]_. Python only.

LOG: Well log conditioning, method='log'
----------------------------------------

``/method='log'`` maps features of a specific model (a realizations of the prior) directly into data. 
Not yet implemented.
  

POST - :samp:`f_post_h5`
========================

At the very minimim POST.h5 needs to conatin the index (in PRIOR.h5) of realizations from the posterior

.. list-table:: Data and features in POST.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset     
     - Format
     - Feature
     - Mandatory
     - Description     
   * - /i_use
     - [N,Nr]
     - 
     - *
     - Index of posterior realizations for each data 
   * - /T
     -  [N,1]
     - 
     - *
     - The annealing temperature used for inversion
   * - /EV
     -  [N,1]
     - 
     - *
     - Evidence
   * - /f5_data
     - F [string]
     - *
     - *
     - Filename of HDF5 data file.
   * - /f5_prior
     - F [string]
     - *
     - *
     - Filename of HDF5 PRIOR file.






Continious parameters
---------------------

For continuous model parameters the follwing generic posterior statistics are computed

.. list-table:: Data and features for continuous parameters in POST.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset     
     - Format
     - Feature
     - Mandatory
     - Description     
   * - /M1/Mean
     - [N,Nm]
     - 
     - 
     - Pointwise mean of the posterior
   * - /M1/Median
     - [N,Nm]
     - 
     - 
     - Poinwise median of the posterior
   * - /M1/Std
     - [N,Nm]
     - 
     - 
     - Pointwise standard deviation of the posterior





Discrete parameters
-------------------


For continuous model parameters the following generic posterior statistics are computed


.. list-table:: Data and features for discrete parameters in POST.h5
   :widths: 10 10 5 5 70 
   :header-rows: 1

   * - Dataset     
     - Format
     - Feature
     - Mandatory
     - Description     
   * - /M1/Mode
     - [N,Nm]
     - 
     - 
     - Pointwise mode of the posterior
   * - /M1/Entropy
     - [N,Nm]
     - 
     - 
     - Poinwise entropy of the posterior
   * - /M1/P
     - [N,Nm,Nclass]
     - 
     - 
     - Pointwise posterior probability of each class.


A typical workflow
==================
1. Setup DATA.h5
   
   * Store the observed data and its associated uncertainty in DATA.h5

2. Setup FORWARD.h5

   * Define the forward problem in FORWARD.h5.

3. Setup PRIOR.h5

   * Generate prior model realizations are store in /M1
   * Use FORWARD.h5 to compute the forward response of the prior realizations.
  
4. Sample the posterior and output POST.h5

5. Update POST.h5 with some statistics computed from the posterior.
