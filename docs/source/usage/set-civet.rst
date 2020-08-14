Usage: SET with CIVET
=====================

Download SET package : TODO LINK


Run civet
---------
::
    input_data = 

    mkdir ~/nf/civet_test
    cd ~/nf/civet_test

    # Use the online CBRAIN tools and Guide
    nextflow-20.04.1-all ~/nf/set_alpha10v0/set-nf/civet-nf/main.nf \
        --civet civet_output/ \
        -with-singularity ~/nf/set_alpha10v0/set_alpha10v0.img \
        -resume

    cd ~/nf/
    sh ~/nf/set_alpha10v0civet-nf/tree_for_tractoflow.sh -f input_data/ -c ~/nf/civet_test -o tractoflow_pve/



Run Tractoflow (-profile civet_pve)
-----------------------
PROFILE :

::

    mkdir ~/nf/tf_test
    cd ~/nf/tf_test

    nextflow-20.04.1-all run ~/nf/set_alpha10v0/tractoflow_stonge/main.nf \
        --root tractoflow_pve/ \
        -dti_shells "0 1000" --fodf_shells "0 1000" \
        -profile civet_pve \
        -with-singularity ~/nf/tractoflow_2.0.0_8b39aee_2019-04-26.img \
        -resume





Run SET Nextflow  (set-nf)
--------------------------
PROFILE :

::

    nextflow-20.04.1-all run ~/nf/set_alpha10v0/set-nf/main.nf \
        --tractoflow tractoflow_output/ \
        --surfaces freesurfer_output/ \
        -profile freesurfer_basic \
        -with-singularity ~/nf/set_alpha10v0/set_alpha10v0.img \
        -resume
