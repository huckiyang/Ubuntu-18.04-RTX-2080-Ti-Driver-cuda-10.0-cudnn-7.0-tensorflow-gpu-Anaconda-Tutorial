# RTX-2080-Ti-CUDA-10.0-cudnn-7.0-pytorch-tensorflow-gpu-pyenv-Ubuntu-16.04-Tutorial-i9-CPU

2019.04.02, Huck Yang with Ubuntu-16

Thanks [Tsai-Hyun-Joong](https://github.com/Tsai-Hyun-Joong/Ubuntu-18.04-RTX-2080-Ti-Driver-cuda-10.0-cudnn-7.0-tensorflow-gpu-Anaconda-Tutorial) for a nice reference. For Ubuntu 16 - since RTX-2080-Ti GPU is too new for most virtual environments (conda, pip), but the GPU card could mostly run stably with CUDA 10.0. After endless trying and erasing the disk, I made a modification setting note here. Feel free to leave commit by push commit. 


### Keep these good setting references in the advance. 

   [1. CUDA-10-0-for-rtx-2080-ti-gpu-on-ubuntu-18-04](https://medium.com/@avinchintha/how-to-install-nvidia-drivers-and-cuda-10-0-for-rtx-2080-ti-gpu-on-ubuntu-16-04-18-04-ce32e4edf1c0) 

   [2. ubuntu 18-CUDA10-7.3](https://medium.com/@vitali.usau/install-cuda-10-0-cudnn-7-3-and-build-tensorflow-gpu-from-source-on-ubuntu-18-04-3daf720b83fe)

   [3. CUDA-10-tf-gpu](https://www.pytorials.com/how-to-install-tensorflow-gpu-with-cuda-10-0-for-python-on-ubuntu/)

   [4. CUDA-10-ubuntu-18-pytorch](https://vxlabs.com/2018/11/04/pytorch-1-0-preview-nov-4-2018-packages-with-full-cuda-10-support-for-your-ubuntu-18-04-x86_64-systems/)




* # Ubuntu-16 Setting

    ```sudo apt-get update ```

    ```sudo apt-get upgrade```

    ``` sudo apt-get install gcc g++ make cmake git```
    
    ``` sudo apt-get install ```


* # Before NVIDIA Driver Installation

    * Disable the Nouveau Drivers
    
        ``` sudo vim /etc/modprobe.d/blacklist-nouveau.conf ```
    
    * Add the following two lines to the file
    
        ``` blacklist nouveau ```
        
        ``` options nouveau modeset=0 ```
     
    * Regenerate the kernel initramfs
    
        ``` sudo update-initramfs -u ```
        
    * Reboot
    
        ``` reboot ```

* # NVIDIA Driver Installation

    * Version: 410
    
    * 410 Link: https://www.nvidia.com/download/driverResults.aspx/138279/en-us
    
    * Make sure you have logout from Ubuntu
         1. Hit Ctrl+Alt+F1 and login using your credentials.
         ``` sudo service lightdm stop ```
         ``` sudo init 3 ```
    * Installation instructions

        ``` chmod +x NVIDIA-Linux-x86_64-410.78.run ```

        ``` sudo ./NVIDIA-Linux-x86_64-410.78.run ```
        ``` sudo service lightdm start ```
        
    * Reboot
    
        ``` reboot ```
        2. Hit Ctrl+Alt+F7 for coming back GUI
        
    * Test if driver is successfully installed, run:
    
        ``` nvidia-smi ```
        
        ``` nvidia-settings ```
        
        If there are some troubles, remove the driver, and run the installer:
        
        ``` sudo apt-get remove --purge nvidia* ```
        
        ``` sudo ./NVIDIA-Linux-x86_64-410.78.run --no-opengl-files ```
        
* # CUDA
    
    * Version: CUDA 10.0 see the archive
    
    * Cuda link: https://developer.nvidia.com/cuda-10.0-download-archive
    
    * Make sure you have logout from Ubuntu
         1. Hit Ctrl+Alt+F1 and login using your credentials.
         ``` sudo service lightdm stop ```
         ``` sudo init 3 ```
    
    * Cuda installation instructions

        ``` sudo sh cuda_10.0.130_410.48_linux.run ```
        ``` sudo service lightdm start ```
    
    * Set up the development environment (./cuda-10.0/)
    
        ``` sudo vim ~/.bashrc ```

        ``` export PATH=/usr/local/cuda-10.0/bin${PATH:+:${PATH}}```
        
        ``` export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}} ```
        
        ``` source ~/.bashrc ```
        
    * Test if CUDA is successfully installed, run:
    
        ``` nvcc -V ```
        

        If there are some troubles, remove CUDA, and run the installer:
        
        ``` cd /usr/local/cuda/bin ```
        
        ``` sudo ./uninstall_cuda_10.0.pl ```
        
        ``` sudo ./NVIDIA-Linux-x86_64-410.78.run --no-opengl-libs ```

* # cuDNN

    * Version: cuDNN v7.4.1

    * cuDNN link: https://developer.nvidia.com/rdp/cudnn-archive
    
    * Unzip the cuDNN package
        
        ``` tar -xzvf cudnn-10.0-linux-x64-v7.4.1.5 ```
        
    * Copy the files into the CUDA Toolkit directory
    
        ``` sudo cp cuda/include/cudnn.h /usr/local/cuda/include ```
        
        ``` sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64 ```
        
        ``` sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn* ```

* # Pyenv is coming
    
    * using pyenv to regulate your environment

            
* # Congratulations! 

* Feel free to star. 
