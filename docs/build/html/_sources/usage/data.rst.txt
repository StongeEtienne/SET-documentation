Data Requirements
=================

Data for freesurfer
-------------------



Data for CIVET
--------------




Data for Tractoflow
--------------------------

::

    [root folder as input]
    ├── S1
    │   ├── brain_mask.nii.gz
    │   ├── bval
    │   ├── bvec
    │   ├── dwi.nii.gz
    │   ├── t1.nii.gz
    │   ├── rev_b0.nii.gz  (optional)
    │   └── pve_wm.nii.gz*  (with civet_pve or fsl_pve)
    │   └── pve_gm.nii.gz*  (with civet_pve or fsl_pve)
    │   └── pve_csf.nii.gz* (with civet_pve or fsl_pve)
    │   └── pve_sc.nii.gz*  (with civet_pve)
    └── S2
        ├── brain_mask.nii.gz
        ├── ...


Standard profile
++++++++++++++++


-profile brain_mask_only
++++++++++++++++++++++++


-profile civet_pve
++++++++++++++++++


-profile fsl_pve
++++++++++++++++++
