Usage and Run Instructions
=====


General Usage
------------

.. code-block:: console

   sca-motion-parcellation.py --dicom --MRN --study_date --license --heuristic --atlas_path --atlas_label

Example Usages
----------------

.. code-block:: console

   sca-motion-parcellation.py --dicom=/home/nick/bids_atlas_test_4/4028832-sorted-5-with-sca-motion-parcellation-working-3/ --MRN=4028832 --study_date=20240716 --license=/home/nick/bids_atlas_test/license.txt --heuristic=/home/nick/bids_atlas_test_4/heuristic_pacs.py --atlas_path=/home/nick/dicom_sca_pipe/c4028832_s20240716_ParcellationNVM.nrrd --atlas_label=/home/nick/dicom_sca_pipe/NVM_Parcellation_description.txt

Or

.. code-block:: console

   sca-motion-parcellation.py --dicom=/home/nick/bids_atlas_test_4/4028832-sorted-5-with-sca-motion-parcellation-working-3/ --MRN=4028832 --study_date=20240716 --license=/home/nick/bids_atlas_test/license.txt --heuristic=/home/nick/bids_atlas_test_4/heuristic_pacs.py 


Explaination of Inputs
----------------

***--dicom (Required) Dicom Sorted Data File Path***
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




