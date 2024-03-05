# INTEGRATE workflow

## Create realizations from the prior and store in PRIOR.h5

The Duagaard type prior results in 3 types of model parameters stored as 

    PRIOR.h5:/M1
    PRIOR.h5:/M2
    PRIOR.h5:/M2

## Compute prior data and store in PRIOR.h5

### Compute prior EM data 

    PRIOR.h5:/M1
    PRIOR.h5:/M2
    PRIOR.h5:/M2
    PRIOR.h5:/D1 --> EM data
    
### Compute prior lithology data 

    PRIOR.h5:/M1
    PRIOR.h5:/M2
    PRIOR.h5:/M2
    PRIOR.h5:/D1
    PRIOR.h5:/D2 --> lithology 'data'

