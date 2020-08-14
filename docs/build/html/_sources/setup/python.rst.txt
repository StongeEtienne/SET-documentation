Python
======

Only for courageous people that really love python.
Guide to setup python to run/develop SET-pipeline without singularity image

Requirements
------------

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



Annaconda
---------

::

    wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
    bash Anaconda3-2020.07-Linux-x86_64.sh

    source ~/.bashrc
    # Remove the default install  (ALWAYS USE ENVIRONMENT)
    conda config --set auto_activate_base false




Python 3.7 (for tractoflow, scilpy)
-----------------------------------

::

    conda create -n set37 python=3.7
    conda activate set37

    cd ~
    mkdir src/
    cd src/
    git clone https://github.com/scilus/scilpy.git scilpy
    cd scilpy
    pip install -e .

    conda install matplotlib ipython jupyter



Python 2.7 (for set, scilpy_old)
--------------------------------

::

    conda create -n set27 python=2.7
    conda activate set27

    conda install numpy scipy matplotlib ipython jupyter cython

    pip install h5py==2.9.0
    pip install imageio==2.4.1
    pip install moviepy==0.2.3.5
    pip install openpyxl==2.4.8
    pip install pandas==0.20.3
    pip install Pillow==5.2.0
    pip install requests==2.19.1
    pip install scikit-learn==0.19.0
    pip install vtk==8.1.2
    pip install PyMCubes==0.0.9
    pip install nibabel==2.4.0
    pip install git+https://github.com/MarcCote/tractconverter@master#tractconverter
    pip install fury==0.4.0
    pip install dipy==0.16.0

    cd ~
    mkdir src/
    cd src/
    git clone ${SCILPYB} scilpy_b
    cd scilpy_b

    python setup.py build_all
    pip install -e .
