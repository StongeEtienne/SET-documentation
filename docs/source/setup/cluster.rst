Setup on cluster
================

Linux based system only

Requirements (bashrc, or run script)
------------------------------------

::

    module load java/1.8.0_121
    module load singularity/3.5

    export _JAVA_OPTIONS=-Xmx512m
    export JVM_OPTS="-server -Xmx512m -Xmx512m"



Singularity config file (singularity.conf)
------------------------------------------

::

    singularity.runOptions="--bind /full_path_to/scratch/user/nf,/full_path_to/scratch/user/data"
    process.executor='ignite'
