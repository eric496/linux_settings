# Linux Settings
system settings and tricks for ubuntu 16.04 with a GTX 1070/1080 GPU

## Nvidia driver for GTX 1070/1080
1. install ubuntu 16.04 without GPU
2. sudo apt-get update
3. download [367.27](http://www.nvidia.com/download/driverResults.aspx/104284/en-us)
4. shut down and plug in GPU
5. start and press "esc" to grub2 window
6. hightlight "Ubuntu" and press "e" to edit: add "nomodeset" after "ro" (with space) in the "linux" line, then press f10 to start
7. (screen flickering) right click mouse and open terminal: type "sudo chvt 1" and login
8. sudo service lightdm stop and
9. install 367.27
10. sudo service lightdm start


## Deep learning setup
After step 2 in the previous section

1. install CUDA 8.0 RC (https://developer.nvidia.com/cuda-release-candidate-download). Note you need to create an account first
2. install cuDNN v5 for CUDA 8.0 RC (https://developer.nvidia.com/rdp/cudnn-download)
3. remove driver v.361 (to avoid deep learning library conflict later we need to explictly delete driver v.361)
	
	sudo apt-get remove --purge nvidia-361 

## Keras with Theano backend
1. sudo pip install keras
2. Create a file ~/.theanorc with following contents

	[global]

	floatX = float32
	
	device = gpu0


	[nvcc]
	
	fastmath = True

        [lib]
        
        cnmem = 0.9



## caffe
1. refer to this: https://github.com/saiprashanths/dl-setup. but before 'make all' and 'make test', modify the Makefile.config:

	INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/

	LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/


## blank screen
1. sudo /usr/bin/
2. gnome-terminal
3. ccsm
4. "Enable Unity Desktop" - For any conflict, just diable the settings in "General"


## fish
set fish env var:

set -U fish_user_paths $fish_user_paths my_path

for example: set -U fisher_user_paths $fish_user_paths ~/anaconda2/bin/

## disable "system program problem detected" dialog
1. sudo rm /var/crash/*
2. vim /etc/default/apport
3. change "enable=1" to "enable=0"
4. sudo service apport stop
5. restart

## git credential setting
1. $ git config credential.helper store
2. $ git push http://example.com/repo.git
3. Username: <type your username>
4. Password: <type your password>

## install mxnet
1. sudo apt-get update
2. sudo apt-get install -y build-essential git libatlas-base-dev libopencv-dev
3. git clone --recursive https://github.com/dmlc/mxnet
4. cd mxnet/make/config.mk
5. change these lines:
   
   ADD_LDFLAGS = -I/usr/local/openblas/lib
   
   ADD_CFLAGS =  -I/usr/local/openblas/include

   USE_CUDA = 1
 
   USE_CUDNN = 1
   
   USE_CUDA_PATH = /usr/local/cuda-8.0

   USE_BLAS = openblas

6. cd mxnet; make -j4
7. cd mxnet/python; python setup.py install
