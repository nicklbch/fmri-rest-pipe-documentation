Outputs and Output Conventions 
=====

In the sorted directory, the SCA-motion pipeline will create the following files / folders:

**BID,  final_outputs,  heuristic_pacs.py,  participant_sub-<MRN>,  __pycache__,  ses-<study_date>**

The desired final outputs will all be placed in the final_outputs folder, with other folders kept for debugging or computational purposes

final_outputs
------------

The final_outputs will contain the following files / folders. 

**motion_output,  sca_output,  sub-<MRN>_ses-<study_date>_task-rest_bold.json  sub-<MRN>_ses-<study_date>_task-rest_bold.nii.gz  working**

**motion_output**
_________________

This folder contains all transforms as .tfm files created via the slice-volume motion analysis. This folder also contains another folder named **sliceTransformalign-0000-0000_outputs** that contains motion monitoring results based upon the transforms. These outputs are further discussed in https://github.com/josh-auger/motion-monitor


**sca_output**
______________

This folder contains a square N x N numpy array of seed correlations called **np_correlation_matrix.npy** nd the set of N labels used as regions within the correlation called **atlas_labels.txt** . This is graphically represented in NifTi Seed Correlations of every region saved as convention sca_full.png. The individual correlation NifTis are also saved here as convention **sca_corellation_np_single_<Label Region>.nii.gz**

The **working, sub-<MRN>_ses-<study_date>_task-rest_bold.json and sub-<MRN>_ses-<study_date>_task-rest_bold.nii.gz** are used for debugging and computational purposes for the motion analysis. 

Additional Outputs
------------

The following outputs are created for debugging or computational purposes.

**BID:** This folder contains the DICOM data in BIDS format using heudiconv

**participant_sub-<MRN>:** This folder contains the data processed from the BIDS format by fmriprep into various transformed data and confounds (The outputs of fmriprep). See https://fmriprep.org/en/latest/outputs.html for more information

**heuristic_pacs.py:** The heuristic file input copied over for computational usage.

**__pycache__:** Python cache

**ses-<study_date>:** Folder containing key fmriprep outputs used for computation.


