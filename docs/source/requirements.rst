Requirements
=====


Docker Dependencies
------------

The following docker images must be available and added to the environment 

● sms-mi-reg Docker Container: https://github.com/ComputationalRadiology/sms-mi-reg/

● motion-monitor Docker Container: https://github.com/josh-auger/motion-monitor

● heudiconv Docker Container: https://hub.docker.com/r/nipy/heudiconv

● fmriprep Docker Container: https://hub.docker.com/r/nipreps/fmriprep

Python Package Requirements
----------------
The following python must be available and added to the environment, this can often be gotten via 
.. code-block:: console

   pip3 install <package>

● nibabel
● os
● numpy as np
● pandas as pd
● from nilearn  datasets
● from nilearn  plotting
● from nilearn  surface
● from nilearn.connectome  ConnectivityMeasure
● from nilearn.maskers  NiftiLabelsMasker
● matplotlib.pyplot as plt
● subprocess
● json
● SimpleITK as sitk
● scipy.stats as st
● sys
● argparse
● os
● glob
● from collections  OrderedDict
● re



