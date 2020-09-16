# SurfaceVolumeMeshingToolKit

Clone SVMTK with the flag '--recursive' to also clone the submodules Pybind11 and CGAL.
Alternatively run `git submodule update --init`.

## Additional requirements

The installation of SVMTK requires the following:  
 - Python>=3.6
 - EIGEN >= 3.2
 - CMake >= 3.5 
 - GMP   
 - MPFR
 - boost   
 - C++>=7

## Installing requirements
   see [REQUIREMENTS.md](REQUIREMENTS.md)


## Configure Pybind11

The relevant files can be found in external/pybind11 after

`git clone --recursive https://github.com/SVMTK/SVMTK`

The submodule can be updated with

`git submodule update` --init

or submodule version switched with

`cd external/pybind11`
`git checkout version`

### Configure CGAL

The relevant files can be found in external/cgal after 

`git clone --recursive https://github.com/SVMTK/SVMTK`

The submodule can be updated with 

`git submodule update`

or submodule version switched with 

`cd external/cgal`
`git checkout releases/CGAL-5.0.3`

Tested CGAL versions 
  - 5.0.3
  - 5.0.2

## Installation

First, ensure that all of the prerequisites needed by SVMTK are installed. 

Installation instructions for all of the SVMTK requirements can be found in [REQUIREMENTS.md](REQUIREMENTS.md)

Next, clone the SVMTK repository by 

`git clone --recursive https://github.com/SVMTK/SVMTK`

If you have already installed SVMTK you can update your installation with the following command executed in the /SVMTK directory

`git submodule update --init`

Third, you will need to setup SVMTK. To do this you can execute 

`python3 setup.py install`

from within the SVMTK directory.

You may see warnings as the setup process runs; these warnings arise from the CGAL source code, which is used by SVMTK, and are no cause for concern.

Finally, you can test your SVMTK installation by running
 
`python3 setup.py test`

Note that, if you do not use a virtual environment, you may need to preface the above commands, for setting up and testing SVMTK, with the `sudo' keyword.  Thus, 

`sudo python3 setup.py install`

and

`sudo python3 setup.py test`

respectively.

If the test is successful you should see the following output 

`----------------------------------------------------------------------`
`Ran 43 tests in XXXX s`

`OK`

Also check the installation with any of the examples in `examples/`

## Docker

There is a Dockerfile in `docker/`

For more information on how to use docker, take a look at the docker tutorial:
[https://docs.docker.com/get-started/]

## Build instructions on SAGA HPC Cluster

`export PROJECT_HOME=path-to-base-install-dir`

`module load Python/3.7.4-GCCcore-8.3.0 CMake/3.12.1 GCC/8.3.0 Boost/1.71.0-GCC-8.3.0 Eigen/3.3.7 MPFR/4.0.2-GCCcore-8.3.0.lua GMP/6.1.2-GCCcore-8.3.0.lua`

`export CMAKE_PREFIX_PATH=$PROJECT_HOME/src/SVMTK/local:/cluster/software/Eigen/3.3.7:/cluster/software/Boost/1.71.0-GCC-8.3.0:/cluster/software/MPFR/4.0.2-GCCcore-8.3.0:/cluster/software/GMP/6.1.2-GCCcore-8.3.0`

`cd SVMTK/external/pybind11/`

`mkdir build`

`cd build/`

`cmake -DPYBIND11_TEST=off -DCMAKE_INSTALL_PREFIX=$PROJECT_HOME/src/SVMTK/local ..`

`make install`

`cd ../..`

`curl -sL https://github.com/CGAL/cgal/releases/download/releases%2FCGAL-5.0.3/CGAL-5.0.3.tar.xz | tar -xJf -`

`cd CGAL-5.0.3/`

`mkdir build`

`cd build/`

`cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$PROJECT_HOME/src/SVMTK/local -DWITH_Eigen3:BOOL=ON .. && make -j4`

`make install`

`cd ../../../`

`mkdir -p $PROJECT_HOME/src/SVMTK/local/lib/python3.7/site-packages/`

`export PYTHONPATH=$PROJECT_HOME/src/SVMTK/local/lib/python3.7/site-packages:$PYTHONPATH`

`python setup.py install --prefix=$PROJECT_HOME/src/SVMTK/local`

### Running SVMTK on SAGA HPC Cluster

`export PROJECT_HOME=path-to-base-install-dir`

`module load Python/3.7.4-GCCcore-8.3.0 CMake/3.12.1 GCC/8.3.0 Boost/1.71.0-GCC-8.3.0 Eigen/3.3.7 MPFR/4.0.2-GCCcore-8.3.0.lua GMP/6.1.2-GCCcore-8.3.0.lua`

`export PYTHONPATH=$PROJECT_HOME/src/SVMTK/local/lib/python3.7/site-packages:$PYTHONPATH`

`python -c "import SVMTK"`

## About

SVMTK is written by Lars Magnus Valnes and Jakob Schreiner
