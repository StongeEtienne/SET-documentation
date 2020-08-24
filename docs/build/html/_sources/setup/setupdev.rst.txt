Setup  dev (without singularity)
================================

tested on Linux : Ubuntu 16.04-18.04 and Mint 18-19

Requirements
------------

::

    sudo sed -i 's/main/main restricted universe/g' /etc/apt/sources.list
    sudo apt-get update && apt-get -y upgrade
    sudo apt-get -y  install wget
    sudo wget -O- http://neuro.debian.net/lists/xenial.us-ca.full | tee /etc/apt/sources.list.d/neurodebian.sources.list
    sudo apt-key adv --recv-keys --keyserver pool.sks-keyservers.net 2649A5A9 || { wget -q -O- http://neuro.debian.net/_static/neuro.debian.net.asc | apt-key add -; }
    sudo apt-get update
    sudo apt-get -y install git
    sudo apt-get -y install build-essential
    sudo apt-get -y install zlib1g-dev
    sudo apt-get -y install g++
    sudo apt-get -y install gcc
    sudo apt-get -y install libc6
    sudo apt-get -y install libstdc++6
    sudo apt-get -y install imagemagick
    sudo apt-get -y install perl
    sudo apt-get -y install p7zip-full

    sudo apt-get -y install python
    sudo apt-get -y install python-dev
    sudo apt-get -y install python-pip
    sudo apt-get -y install python-tk

    sudo apt-get -y install libeigen3-dev
    sudo apt-get -y install libqt4-opengl-dev
    sudo apt-get -y install libgl1-mesa-dev
    sudo apt-get -y install libfftw3-dev
    sudo apt-get -y install libtiff5-dev
    sudo apt-get -y install clang
    sudo apt-get -y install libblas-dev liblapack-dev
    sudo apt-get -y install libgsl0-dev
    sudo apt-get -y install libgsl2
    sudo apt-get -y install xvfb

    sudo apt-get -y install fsl-5.0-eddy-nonfree=5.0.9-1~nd16.04+1

    pip install --upgrade pip==20.1
    pip install setuptools==40.2.0


Python
---------------------------------------

See python section



Other tools (ANTs, MRtrix3, Freesurfer)
---------------------------------------

::

    # Cmake
    cd ~/opt
    wget https://github.com/Kitware/CMake/releases/download/v3.13.2/cmake-3.13.2.tar.gz
    tar -xvzf cmake-3.13.2.tar.gz
    rm -f cmake-3.13.2.tar.gz
    cd cmake-3.13.2
    ./bootstrap
    make -j 6
    make install

    # FSL
    wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_openmp
    chmod +x eddy_openmp
    mv eddy_openmp /usr/share/fsl/5.0/bin/eddy_openmp

    wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
    dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
    apt-get update
    DEBIAN_FRONTEND=noninteractive apt-get -y install cuda-runtime-8-0

    wget https://fsl.fmrib.ox.ac.uk/fsldownloads/patches/eddy-patch-fsl-5.0.11/centos6/eddy_cuda8.0
    chmod +x eddy_cuda8.0
    mv eddy_cuda8.0 /usr/share/fsl/5.0/bin/eddy_cuda

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

    # MRtrix
    cd ~/opt
    git clone https://github.com/MRtrix3/mrtrix3.git
    cd mrtrix3
    git fetch --tags
    git checkout tags/3.0_RC3 -b 3.0_RC3
    ./configure
    ./build

    # Freesurfer
    cd ~/opt
    wget https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    tar zxvf freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    rm freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
    sed -i "s/source $FREESURFER/bash $FREESURFER/g" /freesurfer/freesurfer/SetUpFreeSurfer.sh

    echo "TODO :  mv license.txt opt/freesurfer/"


    # PATH variables
    echo 'export PATH=${HOME}/opt/mrtrix3/bin:$PATH' >> ~/.bashrc

    echo 'export ITK_GLOBAL_DEFAULT_NUMBER_OF_THREADS=8' >> ~/.bashrc
    echo 'export ANTSPATH=${HOME}/opt/ants_build/bin' >> ~/.bashrc
    echo 'export PATH=$PATH:$ANTSPATH' >> ~/.bashrc

    echo 'export FREESURFER_HOME=${HOME}/opt/freesurfer/' >> ~/.bashrc
    echo 'export SUBJECTS_DIR=$FREESURFER_HOME/subjects' >> ~/.bashrc
    echo 'export FUNCTIONALS_DIR=$FREESURFER_HOME/sessions' >> ~/.bashrc
    echo 'export FSFAST_HOME=$FREESURFER_HOME/fsfast' >> ~/.bashrc
    echo 'export MNI_DIR=$FREESURFER_HOME/mni' >> ~/.bashrc
    echo 'export MINC_BIN_DIR=$FREESURFER_HOME/mni/bin' >> ~/.bashrc
    echo 'export MINC_LIB_DIR=$FREESURFER_HOME/mni/lib' >> ~/.bashrc
    echo 'export MNI_PERL5LIB=$FREESURFER_HOME/mni/share/perl5' >> ~/.bashrc
    echo 'export PERL5LIB=$MNI_PERL5LIB' >> ~/.bashrc
    echo 'export LOCAL_DIR=$FREESURFER_HOME/local' >> ~/.bashrc

    echo 'export PATH=$FREESURFER_HOME/bin:$FSFAST_HOME/bin:$PATH' >> ~/.bashrc
    echo 'export PATH=$MINC_BIN_DIR:$PATH' >> ~/.bashrc

    echo 'export FSLDIR=/usr/share/fsl/5.0' >> ~/.bashrc
    echo 'source ${FSLDIR}/etc/fslconf/fsl.sh' >> ~/.bashrc
    echo 'export PATH=${FSLDIR}/bin:${PATH}' >> ~/.bashrc
    echo 'export OPENBLAS_NUM_THREADS=1' >> ~/.bashrc


MINC tools (CIVET)
------------------

::

    wget http://packages.bic.mni.mcgill.ca/minc-toolkit/Debian/minc-toolkit-1.9.16-20180117-Ubuntu_16.04-x86_64.deb
    wget http://packages.bic.mni.mcgill.ca/minc-toolkit/Debian/beast-library-1.1.0-20121212.deb
    wget http://packages.bic.mni.mcgill.ca/minc-toolkit/Debian/bic-mni-models-0.1.1-20120421.deb
    dpkg -i minc-toolkit-1.9.16-20180117-Ubuntu_16.04-x86_64.deb beast-library-1.1.0-20121212.deb bic-mni-models-0.1.1-20120421.deb
    rm -f minc-toolkit-1.9.16-20180117-Ubuntu_16.04-x86_64.deb beast-library-1.1.0-20121212.deb bic-mni-models-0.1.1-20120421.deb


CIVET Labels
------------------

civet2_dkt.tar.bz2 & civet2_aal.tar.bz2

::

    mkdir  ~/src_set/civet2_dkt
    mkdir  ~/src_set/civet2_aal
    tar -jxf civet2_dkt.tar.bz2 -C $SINGULARITY_ROOTFS/civet2_dkt
    tar -jxf civet2_aal.tar.bz2 -C $SINGULARITY_ROOTFS/civet2_aal