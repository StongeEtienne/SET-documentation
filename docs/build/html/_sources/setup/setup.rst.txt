Setup
=====

Linux based system only


::
    sudo apt-get update && sudo apt-get install -y \
        build-essential \
        uuid-dev \
        libgpgme-dev \
        squashfs-tools \
        libseccomp-dev \
        wget \
        pkg-config \
        git \
        cryptsetup-bin

    cd ~/opt
    export VERSION=1.13.5 OS=linux ARCH=amd64 && \
        wget https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz && \
        sudo tar -C /usr/local -xzvf go$VERSION.$OS-$ARCH.tar.gz && \
        rm go$VERSION.$OS-$ARCH.tar.gz

    echo 'export GOPATH=${HOME}/opt/go' >> ~/.bashrc && \
        echo 'export PATH=/usr/local/go/bin:${PATH}:${GOPATH}/bin' >> ~/.bashrc && \
        source ~/.bashrc

    cd ~/opt
    export VERSION=3.5.2 && # adjust this as necessary \
        wget https://github.com/sylabs/singularity/releases/download/v${VERSION}/singularity-${VERSION}.tar.gz && \
        tar -xzf singularity-${VERSION}.tar.gz && \
        cd singularity


    ./mconfig && \
        make -C ./builddir && \
        sudo make -C ./builddir install

    # install  nextflow 20.04.1
    cd ~/opt
    wget https://github.com/nextflow-io/nextflow/releases/download/v20.04.1/nextflow-20.04.1-all
    chmod +x nextflow-20.04.1-all


    # Cmake
    cd ~/opt
    wget https://github.com/Kitware/CMake/releases/download/v3.13.2/cmake-3.13.2.tar.gz
    tar -xvzf cmake-3.13.2.tar.gz
    rm -f cmake-3.13.2.tar.gz
    cd cmake-3.13.2
    ./bootstrap
    make -j 6
    make install


    # ANTs
    cd ~/opt
    mkdir ants_build
    git clone https://github.com/ANTsX/ANTs.git
    cd ANTs
    git fetch --tags
    git checkout tags/v2.3.1 -b v2.3.1
    cd ../ants_build
    cmake ../ANTs
    make -j 6
    cp ../ANTs/Scripts/*.sh bin/


    # Freesurfer
    cd ~/opt
    wget https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    tar zxvf freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    rm freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    sed -i "s/source $FREESURFER/bash $FREESURFER/g" /freesurfer/freesurfer/SetUpFreeSurfer.sh

    echo "TODO :  mv license.txt opt/freesurfer/"

    # MRtrix
    cd ~/opt
    git clone https://github.com/MRtrix3/mrtrix3.git
    cd mrtrix3
    git fetch --tags
    git checkout tags/3.0_RC3 -b 3.0_RC3
    ./configure
    ./build
