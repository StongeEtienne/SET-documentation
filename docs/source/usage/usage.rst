Usage
=====

::

    nextflow-20.04.1-all run ~/nf/set_alpha10v0/set-nf/main.nf \
        --tractoflow tractoflow_output/ \
        --surfaces freesurfer_output/ \
        -profile freesurfer_basic \
        -with-singularity ~/nf/set_alpha10v0/set_alpha10v0.img \
        -resume
