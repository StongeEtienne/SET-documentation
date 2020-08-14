Usage
=====

::

    nextflow -c /scratch/stoeti/src/singularity.conf run /scratch/stoeti/src/set_alpha10v0/tractoflow_stonge/main.nf --root /scratch/stoeti/data/hcp_tr/hcp_tractoflow_fsl_input_test/ -profile brain_mask_only --dti_shells '0 1000' --fodf_shells '0 1000 2000 3000' --run_topup false --run_eddy false --run_resample_dwi false --sh_order 8 --set_frf true --manual_frf 15,4,4 --run_ants_warp_t1 false run_resample_t1 false --run_denoise_t1 true --run_n4_t1 false --run_dwi_denoising true --processes_denoise_dwi 8 -with-report report.html -with-singularity /scratch/stoeti/src/tractoflow_2.0.0_8b39aee_2019-04-26.img -resume -with-mpi
