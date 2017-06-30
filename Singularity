Bootstrap: docker
From: ubuntu:16.04

%setup
/bin/bash functions/download_data.sh

%files
-R analysis/* /code/analysis
-R data/input/* /data/input

%labels
CONTAINERSFTW_TEMPLATE ubuntu16.04-python2
CONTAINERSFTW_COMPETITION_HOST containersftw
CONTAINERSFTW_COMPETITION_NAME 

%environment
CONTAINERSFTW_DATA=/data/input
CONTAINERSFTW_RESULT=/code/analysis/results/submission
CONTAINERSFTW_WORK=/code/analysis
export CONTAINERSFTW_DATA
export CONTAINERSFTW_RESULT
export CONTAINERSFTW_WORK

%runscript

     # This will generate the scientific result!
     /usr/bin/python /code/analysis/main.py

%post
     
     # Data directories
     mkdir -p /data/input   # data included with container
     mkdir -p /data/work    # working directory
     mkdir -p /data/mnt     # mounted datasets

     # Result directories
     mkdir -p /code/results/submission
     mkdir -p /code/results/web
     mkdir -p /code/results/pub

     # Working code directories
     mkdir -p /code/analysis
     mkdir -p /code/tests

     # Download evaluation functions

     apt-get update && apt-get install -y python git vim nginx wget
     wget https://bootstrap.pypa.io/get-pip.py
     python get-pip.py && rm get-pip.py
     pip install -y numpy scipy pandas scikit-learn ipython
     
     #########################################################
     # Install additional software / libraries here
     #########################################################


     #########################################################

     apt-get autoremove -y
     apt-get clean
