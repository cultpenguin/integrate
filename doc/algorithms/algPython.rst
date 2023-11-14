=================
Python Algorithms 
=================


integrate_rejection 
-------------------
This function implements the rejection sampler 

..  code-block:: python
    :caption: EXT:site_package/Configuration/TCA/Overrides/sys_template.php
    
    integrate_rejection.py [f_prior_h5] [f_data_h5] [-h] [--autoT AUTOT] [--N_use N_USE] [--ns NS] [--parallel PARALLEL] 

By default `autoT=1`, `N_use=1000000`, `ns=1000`, and `parallel=1`.	

For example, to use the prior models and data in `DJURSLAND_P01_N0010000_NB-13_NR03_PRIOR.h5` and the data in `tTEM-Djursland.h5`, run

..  code-block:: python
    :caption: EXT:site_package/Configuration/TCA/Overrides/sys_template.php

    python integrate_rejection.py DJURSLAND_P01_N0010000_NB-13_NR03_PRIOR.h5 tTEM-Djursland.h5




