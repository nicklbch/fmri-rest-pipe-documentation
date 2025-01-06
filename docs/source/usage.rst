Usage and Run Instructions
=====


General Usage
------------

.. code-block:: console

   sca-motion-parcellation.py --dicom --MRN --study_date --study_name --license --heuristic --atlas_path --atlas_label

Example Usages
----------------

.. code-block:: console

   sca-motion-parcellation.py --dicom=/home/nick/bids_atlas_test_4/4028832-sorted-5-with-sca-motion-parcellation-working-3/ --MRN=4028832 --study_date=20240716 --license=/home/nick/bids_atlas_test/license.txt --heuristic=/home/nick/bids_atlas_test_4/heuristic_pacs.py --atlas_path=/home/nick/dicom_sca_pipe/c4028832_s20240716_ParcellationNVM.nrrd --atlas_label=/home/nick/dicom_sca_pipe/NVM_Parcellation_description.txt

Or

.. code-block:: console

   sca-motion-parcellation.py --dicom=/home/nick/bids_atlas_test_4/4028832-sorted-5-with-sca-motion-parcellation-working-3/ --MRN=4028832 --study_date=20240716 --license=/home/nick/bids_atlas_test/license.txt --heuristic=/home/nick/bids_atlas_test_4/heuristic_pacs.py 


Explaination of Inputs
----------------

**--dicom (Required) Dicom Sorted Data File Path**
_______________________________________

The input required by the pipeline requires a set of sorted formatted DICOM data. For data hosted on the BCH research synapse, this can be achieved via the following commands. 

.. code-block:: console

   sudo docker run --rm -it -u $(id -u):$(id -g) \
--volume `pwd`:/data crl/dicom-tools:latest retrieve_dicoms.py \
--outputDir /data/${MRN} \
--aec SYNAPSERESEARCH --aet PACSDCM --namednode 10.20.2.28 --modality MR \
--subjectID ${MRN} --studyDate ${StudyDate}

.. code-block:: console

   sudo docker run --rm -u $(id -u):$(id -g) -v "`pwd`":/data crl/dicom-tools \
  uncompress_dicoms.py ./${MRN} ./${MRN}-uncompressed


.. code-block:: console

   sudo docker run --rm -u $(id -u):$(id -g) -v "`pwd`":/data crl/dicom-tools \
  sort_dicoms.py ./${MRN}-uncompressed ./${MRN}-sorted


.. code-block:: console

   sudo docker run --rm -u $(id -u):$(id -g) -v "`pwd`":/data crl/dicom-tools \
  dicom_tree_to_nifti.py ./${MRN}-sorted ${MRN}-converted



The sorted folder will be the input path to this argument

If data is not from the research synapse, the DICOM data should be uncompressed and formatted. See https://github.com/ComputationalRadiology/dicom-tools for further notes


**--MRN (Required) Medical Record Number of Participant**
_______________________________________

The MRN or Identification number for the study subject passed as a string. This should be consistent with the dicom sorted data

**--study_date (Required) Study Date**
_______________________________________

The study date for analysis in format YYYYMMDD. This should be consistent with the dicom sorted data

**--study_name (Required) Study Name**
_______________________________________


The study name derived from DICOM sorted data. This can be found by checking the third folder within the DICOM sorted data. MRN/study_date/study_name

**--license (Required) FreeSurfer License File Location**
_______________________________________

The file location of a FreeSurfer License File saved as license.txt. A license can be obtained at https://surfer.nmr.mgh.harvard.edu/registration.html

**--heuristic (Required) HeuDiConv Heuristic Conversion Python File Location**
_______________________________________

HeuDiConv requires a configuration python file to convert dicom data into BIDS compliant data. **This conversion however may differ depending on initial dicom source data.** For the Warfield Atlas data, the following heuristic.py file can be used https://github.com/ComputationalRadiology/sms-mi-reg/blob/main/sca-bmi-motion/sca/heuristic_pacs.py. This may need to be adjusted for the incoming dicom data source. For more information use https://heudiconv.readthedocs.io/en/latest/heuristics.html, https://heudiconv.readthedocs.io/en/latest/custom-heuristic.html, https://heudiconv.readthedocs.io/en/latest/

**--atlas_path (Optional) Specify Atlas / Parcellation for Seed Correlation Analysis**
_______________________________________

Optionally the file location of a nifti or nrrd formatted 3D parcellation. **By default, the SCA will be based upon the Harvard Oxford Atlas with a symmetric split.** Parcellation should be in the native subject space, the Harvard Oxford Atlas will be run in the MNI2009 space. 
**A specified parcellation will only run if both  --atlas_path and --atlas_label are specified. Must specify if using --atlas_label tag**

**--atlas_label (Optional) Specify Atlas / Parcellation Labels for Seed Correlation Analysis**
_______________________________________

Optionally the file location of ITK-SnAP Label Description File corresponding to a nifti or nrrd formatted 3D parcellation. **By default, the SCA will be based upon the Harvard Oxford Atlas with a symmetric split and does not require --atlas_label unless specifying a --atlas_path. A specified parcellation will only run if both  --atlas_path and --atlas_label are specified. Must specify if using --atlas_path tag**

.. code-block:: console

   ITK-SnAP Label Description File Format:
   ################################################
   # ITK-SnAP Label Description File
   # File format: 
   # IDX   -R-  -G-  -B-  -A--  VIS MSH  LABEL
   # Fields: 
   #    IDX:   Zero-based index 
   #    -R-:   Red color component (0..255)
   #    -G-:   Green color component (0..255)
   #    -B-:   Blue color component (0..255)
   #    -A-:   Label transparency (0.00 .. 1.00)
   #    VIS:   Label visibility (0 or 1)
   #    IDX:   Label mesh visibility (0 or 1)
   #  LABEL:   Label description 
   ################################################




