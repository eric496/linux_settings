## Install ubuntu 16.04, cuda 8.0 and cudnn
1. install ubuntu 16.04 without GPU
2. download [CUDA 8.0](https://developer.nvidia.com/cuda-toolkit)
3. ```$sudo apt-get update```
4. shut down and plug in GPU
5. start and press "esc" to grub2 window
6. hightlight "Ubuntu" and press "e" to edit: add "nomodeset" after "ro" (with a trailing space) in the "linux" line, then press f10 to start
7. ```sudo chvt 1```
8. ```$sudo service lightdm stop```
9. ```$sudo bash cuda_8.0.44_linux.run```
10. ```$sudo service lightdm start```
11. install [cuDNN](https://developer.nvidia.com/rdp/cudnn-download)
    
    ```$cd cudnn_foler```
     
    ```$sudo cp -P include/cudnn.h /usr/include```
    
    ```$sudo cp -P lib64/libcudnn* /usr/lib/x86_64-linux-gnu/```
    
    ```$sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*```

12. add PATH to ~/.bashrc

    ```$export PATH="/usr/local/cuda-8.0/bin:$PATH"```

    ```$export LD_LIBRARY_PATH="/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH"```

    ```$sudo ldconfig /usr/local/cuda-8.0/lib64```

## install Anaconda 
    
    $bash Anaconda.sh

## install OpenBLAS
    
    $sudo apt-get install gfortran

    $git clone https://github.com/xianyi/OpenBLAS

    $cd OpenBLAS

    $make FC=gfortran

    $sudo make PREFIX=/usr/local install

error: "cannot find -lgfortran"

solution: ```$sudo ln -s /usr/lib/x86_64-linux-gnu/libgfortran.so.3 /usr/lib/libgfortran.so```

## create conda virtual environment for all machine learning libraries
    
    conda create -n mlenv python=2.7
	
    source activate mlenv

## install tensorflow

    (mlenv)$ conda install -c conda-forge tensorflow

## install theano

1. ```$sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git```

2. ```$pip install --upgrade --no-deps git+git://github.com/Theano/Theano.git```

3. Downgrade g++ to 4.9 (5.3 or later version is not compatible)

    ```$sudo apt-get install g++-4.9```

    ```$sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20```
 
    ```$sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 10```

    ```$sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20```

    ```$sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 10```

    ```$sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30```

    ```$sudo update-alternatives --set cc /usr/bin/gcc```

    ```$sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30```

    ```$sudo update-alternatives --set c++ /usr/bin/g++```

4. Work around a glibc bug
    
    ```echo -e "\n[nvcc]\nflags=-D_FORCE_INLINES\n" >> ~/.theanorc```

5. Add the following to ~/.theanorc

    [global]

        floatX = float32

        device = gpu

    [nvcc]

        flags=-D_FORCE_INLINES

        fastmath = True

    [lib]

        cnmem = 0.9

## install keras

1. ```$git clone https://github.com/fchollet/keras.git```

2. ```$cd keras; $sudo python setup.py install```

## install caffe
1. refer to [this](https://github.com/saiprashanths/dl-setup) but before 'make all' and 'make test', modify the Makefile.config:

    ```INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/```

    ```LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/```

## install mxnet
1. ```$sudo apt-get update```
2. ```$sudo apt-get install -y build-essential git libatlas-base-dev libopencv-dev```
3. ```$git clone --recursive https://github.com/dmlc/mxnet```
4. ```$vim mxnet/make/config.mk```
5. change these lines:

    ```ADD_LDFLAGS = -I/usr/local/openblas/lib```

    ```ADD_CFLAGS =  -I/usr/local/openblas/include```

    ```USE_CUDA = 1```

    ```USE_CUDNN = 1```

    ```USE_CUDA_PATH = /usr/local/cuda-8.0```

    ```USE_BLAS = openblas```

6. ```cd mxnet; make -j4```
7. ```cd mxnet/python; python setup.py install```

## Other settings
-----------------------------------------------------------------------------------
## blank screen
1. ```$sudo /usr/bin/```
2. ```$gnome-terminal```
3. ```$ccsm```
4. "Enable Unity Desktop" - For any conflict, just disable the settings in "General"

## fish
```$set fish env var:```

```$set -U fish_user_paths $fish_user_paths my_path```

for example: set -U fisher_user_paths $fish_user_paths ~/anaconda2/bin/

## disable "system program problem detected" dialog
1. ```$sudo rm /var/crash/*```
2. ```$vim /etc/default/apport```
3. change "enable=1" to "enable=0"
4. ```$sudo service apport stop```
5. ```$sudo reboot```

## git credential setting
1. ```$git config credential.helper store```
2. ```$git push http://example.com/repo.git```
3. Username: <type your username>
4. Password: <type your password>

## Issue: Ubuntu cannot launch Matlab

1. ```$sudo chown username -R ~/.matlab```

2. ```$sudo apt-get install matlab-support```
