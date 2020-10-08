Usage: SET with FreeSurfer
==========================

Download SET package : http://scil.dinf.usherbrooke.ca/en/containers_list/


Run freesurfer
--------------

::

    recon-all


Run Tractoflow Nextflow
-----------------------

::

    mkdir ~/nf/tf_test
    cd ~/nf/tf_test

    nextflow-20.04.1-all run ~/nf/set_1v0/tractoflow_stonge/main.nf \
        --root tractoflow_data/ \
        -dti_shells "0 1000" --fodf_shells "0 1000" \
        -profile PROFILE \
        -with-singularity ~/nf/tractoflow_2.0.0_8b39aee_2019-04-26.img \
        -resume


Run civet-nf
------------

::

    mkdir ~/nf/civet_test
    cd ~/nf/civet_test

    # Use the online CBRAIN tools and Guide
    nextflow-20.04.1-all ~/nf/set_1v0/set-nf/civet-nf/main.nf \
        --civet civet_output/ \
        -with-singularity ~/nf/set_1v0/set_1v0.img \
        -resume

    cd ~/nf/
    sh ~/nf/set_1v0/civet-nf/tree_for_tractoflow.sh -f tractoflow_data/ -c ~/nf/civet_test -o tractoflow_data2/



Run SET Nextflow  (set-nf)
--------------------------

::

    nextflow-20.04.1-all run ~/nf/set_1v0/set-nf/main.nf \
        --tractoflow tractoflow_output/ \
        --surfaces freesurfer_output/ \
        -profile freesurfer_basic \
        -with-singularity ~/nf/set_1v0/set_1v0.img \
        -resume
