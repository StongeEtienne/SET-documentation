Setup with singularity
======================

Linux based system only

Requirements
------------

::

    sudo apt-get update && sudo apt-get install -y \
        build-essential \
        uuid-dev \
        libssl-dev \
        libgpgme-dev \
        squashfs-tools \
        libseccomp-dev \
        wget \
        pkg-config \
        git \
        cryptsetup-bin \
        default-jre

    cd ~/opt
    export VERSION=1.13.5 OS=linux ARCH=amd64 && \
        wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
        sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
        rm go$VERSION.$OS-$ARCH.tar.gz

    echo 'export GOPATH=${HOME}/opt/go' >> ~/.bashrc && \
        echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
        source ~/.bashrc


Singularity
------------

::

    cd ~/opt
    export VERSION=3.5.2 && # adjust this as necessary \
        wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
        tar -xzf singularity-${VERSION}.tar.gz && \
        cd singularity

    ./mconfig && \
        make -C ./builddir && \
        sudo make -C ./builddir install



Nextflow
--------

::

    cd ~/opt
    wget https://github.com/nextflow-io/nextflow/releases/download/v20.04.1/nextflow-20.04.1-all
    chmod +x nextflow-20.04.1-all
    echo 'export PATH=${HOME}/opt:${PATH}' >> ~/.bashrc

