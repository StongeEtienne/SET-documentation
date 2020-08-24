Python
======

Only for courageous people that really love python.
Guide to setup python to run/develop SET-pipeline without singularity image

Requirements
------------

See Setup for basic requirements

or Setup Dev for full requirements


Annaconda
---------

Always use environments with anaconda.

::

    wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh
    bash Anaconda3-2020.07-Linux-x86_64.sh

    source ~/.bashrc
    # Remove the default install
    conda config --set auto_activate_base false




Python 3.7 (for scilpy DEV)
---------------------------

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



Python 2.7 (for set DEV)
------------------------

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
    pip install trimeshpy==0.0.2

    cd ~
    mkdir src/
    cd src/
    git clone ${SCILPYB} scilpy_b
    cd scilpy_b

    python setup.py build_all
    pip install -e .




Python 2.7 (for set-nf)
------------------------
set_dipy.tar.bz2 & set_scilpy.tar.bz2

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
    pip install cythongsl==0.2.2
    pip install trimeshpy==0.0.2

    # unzip packages
    mkdir ~/src_set
    mkdir ~/src_set/dipy
    tar -jxf set_dipy.tar.bz2 -C ~/src_set/dipy

    mkdir ~/src_set/scilpy
    tar -jxf set_scilpy.tar.bz2 -C ~/src_set/scilpy


    # Install dipy
    cd  ~/src_set/dipy
    pip install .

    # Install scilpy (SET)
    cd /src_set/scilpy
    python setup.py build_all
    #sed -i '38s/.*/backend : Agg/' /usr/local/lib/python2.7/dist-packages/matplotlib/mpl-data/matplotlibrc
    pip install -e .
