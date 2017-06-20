# Installing TensorFlow for CPU | GPU Simplified

Before you start, the instructions assume that you are running a Ubuntu Machine for doing the installation.


## For CPU:

[Step-1] Installing TensorFlow-CPU:

1. To install the CPU version of TensorFlow on your Ubuntu or Mac OS machine you simply follow the instructions listed on the TensorFlow Website.
2. When following Instruction 1, installing ‘Virtualenv’ is the easiest. If you still face issues you can always follow the ‘Docker Installation’ method for Mac OS or Ubuntu.

## For GPU:

**[Step-1] Installing CUDA Toolkit:**

1. Check if your GPU is CUDA Supported at https://developer.nvidia.com/cuda-gpus before proceeding further.
Download CUDA Toolkit from there by following the on screen instructions and select the ‘runfile’(local) when you are about to download the same.

2. Next depending upon your <editor> preference open the terminal [Ctrl+Alt+T] and enter: ```sudo <Your Code Editor> /etc/modprobe.d/blacklist-nouveau.conf```. Once the editor is open add the below lines in the ```blacklist-nouveau.conf``` file:

```
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off

 ```
3. Now close the file ```blacklist-nouveau.conf``` and run in the terminal:
```sudo update-initramfs -u```. [You might get some warnings related to a 3.3 kernel version but it shouldn’t cause an issue]

4. Next you need to get into ‘Text Mode [Runlevel 3]’, for temporary use you can switch your desktop to tty1 using a key combination of Ctrl + Alt + F1 to enter and Ctrl +Alt + F7 to exit.

Once you are in text mode enter: ```sudo sh cuda_<version-no>_linux.run``` and then follow the on-screen instructions by selecting the following options:
 ```
Do you accept the previously read EULA? (accept/decline/quit): accept

Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 375.26?
((y)es/(n)o/(q)uit): y

Install the CUDA 8.0 Toolkit? ((y)es/(n)o/(q)uit): y

Enter Toolkit Location [ default is /usr/local/cuda-8.0 ]: <Enter>

Do you want to install a symbolic link at /usr/local/cuda? ((y)es/(n)o/(q)uit): y

Install the CUDA 8.0 Samples? ((y)es/(n)o/(q)uit): y

Enter CUDA Samples Location [ default is /root ]: [Any location you want]
 ```
5. Now you need to set the correct path in ```.bashrc``` for CUDA, follow the below steps for the same. To open the ```.bashrc``` file:

```<Your Code Editor> ~/.bashrc```

Append the following lines at the bottom of the file:
 ```
### CUDA Toolkit
export CUDA_HOME=/usr/local/cuda-8.0
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
export PATH=${CUDA_HOME}/bin:${PATH}
 ```
6. In order to verify or check if CUDA toolkit is properly installed open the terminal and enter ```nvcc -V``` and it should give an output mentioning the CUDA version.

If it returns an error saying nvcc is not installed than you need to check if the path you have set is correct as well if CUDA Toolkit is properly installed or not.

7. Usually your ```.bashrc``` is automatically sourced when you login or you open a new terminal but as we have manually updated it right now the below small step would be very helpful.
```source ~/.bashrc```



**[Step-2] Installing cuDNN:**



1. This steps will guide you in installing NVIDIA CUDA® Deep Neural Network library (cuDNN). For downloading the same you will need to create a free account with NVIDIA here and then proceed here to download cuDNN.

Select the option: ‘cuDNN v5.1 Library for Linux’ from the list of downloads list as we are installing on a Ubuntu Machine.
Once you have downloaded it cd to the directory where the file is downloaded and run the following commands in the terminal.

tar -zxf cudnn-8.0-linux-x64-v5.1-ga.tgz
cd cuda
sudo cp lib64/* /usr/local/cuda/lib64/
sudo cp include/* /usr/local/cuda/include/

And you are done! You have now installed cuDNN as well as CUDA.



**[Step-3] Installing CUDA Profiling Tools Interface:**




Open the terminal and enter: sudo apt-get install libcupti-dev




**[Step-4] Installing TensorFlow-GPU:**




To install the GPU version of TensorFlow on your Ubuntu or Mac OS machine you simply follow the instructions listed on the TensorFlow Website.

When following Instruction 1, installing ‘Virtualenv’ is the easiest. If you still face issues you can always follow the ‘Docker Installation’ method for Mac OS or Ubuntu.
