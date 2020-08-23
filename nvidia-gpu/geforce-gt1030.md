# Gigabyte GT 1030

+ [Gigabyte GT 1030 Low Profile D4 2G Specs](https://www.cnet.com/products/gigabyte-gt-1030-low-profile-d4-2g-graphics-card-gf-gt-1030-2-gb/)
+ [GIGABYTE GT 1030 Low Profile](https://www.techpowerup.com/gpu-specs/gigabyte-gt-1030-low-profile.b4616)

# Installing Cuda on Ubuntu 16.04

Some useful links:

+ [CUDA toolkit archive](https://developer.nvidia.com/cuda-toolkit-archive)
+ [CUDA Geforce drivers](https://www.nvidia.com/en-us/geforce/drivers/)
+ [CUDA 8.0 Download](https://developer.nvidia.com/cuda-80-ga2-download-archive)
+ [NVIDIA 415 Driver info](https://www.nvidia.com/Download/driverResults.aspx/140282/en-us) 

Install the CUDA toolkit without the drivers:

```
[root@gpu ~]# wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run
[root@gpu ~]# chmod +x cuda_8.0.61_375.26_linux-run
[root@gpu ~]# ./cuda_8.0.61_375.26_linux-run --silent --toolkit --samples
[root@gpu ~]#
```

Install drivers:

```
[root@gpu ~]# add-apt-repository -y ppa:graphics-drivers/ppa
[root@gpu ~]# apt update
[root@gpu ~]# apt install nvidia-415 nvidia-415-dev libcuda1-415
[root@gpu ~]#
```

Check that all is working properly:

```
[root@gpu ~]# nvidia-smi 
Sun Aug 23 23:13:53 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 415.27       Driver Version: 415.27       CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GT 1030     Off  | 00000000:01:00.0  On |                  N/A |
|  0%   36C    P8    N/A /  30W |     61MiB /  1999MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1013      G   /usr/lib/xorg/Xorg                            59MiB |
+-----------------------------------------------------------------------------+
[root@gpu ~]# 
```

Apply cuda patch:

```
[root@gpu ~]# wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/patches/2/cuda_8.0.61.2_linux-run
[root@gpu ~]# chmod +x cuda_8.0.61.2_linux-run
[root@gpu ~]# ./cuda_8.0.61.2_linux-run 
[root@gpu ~]# nvidia-smi
Sun Aug 23 23:23:10 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 415.27       Driver Version: 415.27       CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GT 1030     Off  | 00000000:01:00.0  On |                  N/A |
|  0%   36C    P8    N/A /  30W |     61MiB /  1999MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1013      G   /usr/lib/xorg/Xorg                            59MiB |
+-----------------------------------------------------------------------------+
[root@gpu ~]#
```

Let's check the device:

```
[root@gpu ~]# cd NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery
[root@gpu deviceQuery]# make
[root@gpu deviceQuery]# ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GT 1030"
  CUDA Driver Version / Runtime Version          10.0 / 8.0
  CUDA Capability Major/Minor version number:    6.1
  Total amount of global memory:                 1999 MBytes (2096431104 bytes)
  ( 3) Multiprocessors, (128) CUDA Cores/MP:     384 CUDA Cores
  GPU Max Clock rate:                            1468 MHz (1.47 GHz)
  Memory Clock rate:                             3004 Mhz
  Memory Bus Width:                              64-bit
  L2 Cache Size:                                 524288 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(131072), 2D=(131072, 65536), 3D=(16384, 16384, 16384)
  Maximum Layered 1D Texture Size, (num) layers  1D=(32768), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(32768, 32768), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 10.0, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = GeForce GT 1030
Result = PASS
[root@gpu deviceQuery]# 
```

Add the following to your **.bashrc** or **.bash_profile**:

```
export PATH="$PATH:/usr/local/cuda-8.0/bin"
export LD_LIBRARY_PATH="/usr/local/cuda-8.0/lib64"
```

> Based on [Using the nVidia GT 1030 for CUDA workloads on Ubuntu 16.04](https://medium.com/@samnco/using-the-nvidia-gt-1030-for-cuda-workloads-on-ubuntu-16-04-4eee72d56791)

## Install a kernel which can load the nvidia driver

You can see what kernels can you install:

```
[root@gpu ~]# dpkg-query -L nvidia-415 | grep patch
/usr/lib/nvidia-415/libGLdispatch.so.0
/usr/lib32/nvidia-415/libGLdispatch.so.0
/usr/src/nvidia-415-415.27/patches
/usr/src/nvidia-415-415.27/patches/allow_sublevel_greater_than_5.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.0.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.10.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.11.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.13.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.14.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.18.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.6.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_3.8.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.10.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.14.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.16.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.19.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.20.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.3.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.6.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.7.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.7_amd64_only.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.8.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.9.patch
/usr/src/nvidia-415-415.27/patches/buildfix_kernel_4.9_amd64_only.patch
/usr/src/nvidia-415-415.27/patches/make-use-of-the-new-uapi-framework.patch
/usr/src/nvidia-415-415.27/patches/register-VT-switch-requirements.patch
/usr/src/nvidia-415-415.27/patches/replace-VM_RESERVED-with-VM_DONTEXPAND-and-VM_DONTDU.patch
[root@gpu ~]#
```

So I have installed a 4.10 kernel and made it the defautl boot kernel:

```
[root@gpu ~]# uname -r
4.10.0-35-generic
[root@gpu ~]#
```

## Troubleshouting

Verify that the nvidia-settings package matches your driver version:

```
[root@gpu ~]# dpkg -l | grep nvidia-settings
ii  nvidia-settings                                   418.56-0ubuntu0~gpu16.04.1                      amd64        Tool for configuring the NVIDIA graphics driver
[root@gpu ~]# 
```

# Installing cuDNN

You will need to download it from [NVIDIA](https://developer.nvidia.com/rdp/cudnn-archive). You will need to download the **cuDNN 6.0 for CUDA 8.0**:

* **libcudnn6_6.0.21-1+cuda8.0_amd64.deb**
* **libcudnn6-dev_6.0.21-1+cuda8.0_amd64.deb**

and install them:

```
[root@gpu ~]# dpkg -i libcudnn6_6.0.21-1+cuda8.0_amd64.deb libcudnn6-dev_6.0.21-1+cuda8.0_amd64.deb
``` 

# Install Tensorflow 1 with GPU support

You can check what [Tensorflow version works with cuda 8.0](https://www.tensorflow.org/install/source#tested_source_configurations):

+ **CUDA version**: 8.0
+ **cuDNN version**: 6.0
+ **Python version**: 2.7, 3.3 to 3.6
+ **Tensorflow version**: 1.4.1

To install python 3.6:

```
[root@gpu ~]# add-apt-repository ppa:deadsnakes/ppa
[root@gpu ~]# apt-get update
[root@gpu ~]# apt-get install python3.6 python3.6-dev swig libclblas-dev
[root@gpu ~]# 
```

> http://sixthdoor.com/deep-learning-setup-tensorflow-gpu-1-4-on-ubuntu-16-04/

Install tensorflow and keras:

```
[root@gpu ~]# python3.6 -m pip install --ignore-installed --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.4.1-cp36-cp36m-linux_x86_64.whl 
[root@gpu ~]# python3.6 -m pip install pyopencl
[root@gpu ~]# python3.6 -m pip install pyclblas
[root@gpu ~]# python3.6 -m pip install keras
[root@gpu ~]# 
```

Add the following lines to your **.bashrc**:

```
alias python='/usr/bin/python3.6'
alias pip='/usr/bin/pip3'
```

Start a new shell to check that python 3.6 is your default python version:

```
[jadebustos@gpu ~]$ python --version
Python 3.6.12
[jadebustos@gpu ~]$ 
```

In this way we do not change the default system-wide python version.

To check if tensorflow is working:

```
[jadebustos@gpu ~]$ cat tensorflow-check.py 
#/usr/bin/python3.6

import tensorflow as tf

hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
[jadebustos@gpu ~]$ python -W ignore tensorflow-check.py 
2020-08-24 00:12:00.932879: I tensorflow/core/platform/cpu_feature_guard.cc:137] Your CPU supports instructions that this TensorFlow binary was not compiled to use: SSE4.1 SSE4.2 AVX AVX2 FMA
2020-08-24 00:12:01.004238: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:892] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-08-24 00:12:01.004528: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1030] Found device 0 with properties: 
name: GeForce GT 1030 major: 6 minor: 1 memoryClockRate(GHz): 1.468
pciBusID: 0000:01:00.0
totalMemory: 1.95GiB freeMemory: 1.85GiB
2020-08-24 00:12:01.004543: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1120] Creating TensorFlow device (/device:GPU:0) -> (device: 0, name: GeForce GT 1030, pci bus id: 0000:01:00.0, compute capability: 6.1)
b'Hello, TensorFlow!'
[jadebustos@gpu ~]$
```

> It is working but we have some warnings ...





# OLD








## Installing python3 and jupyter notebook on Ubuntu 16.04

```
root@lezo:~# apt install software-properties-common
root@lezo:~# add-apt-repository ppa:deadsnakes/ppa
root@lezo:~# apt install python3.7
root@lezo:~# apt install python3.7
root@lezo:~# update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
root@lezo:~# update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
root@lezo:~# python3 -m pip install jupyter
root@lezo:~# python2 -m pip install ipykernel
root@lezo:~# python2 -m ipykernel install --user
root@lezo:~# python3 -m pip install ipykernel
root@lezo:~# python3 -m ipykernel install --user
root@lezo:~# apt-get -y install ipython ipython-notebook
root@lezo:~# apt-get -y install ipython3 ipython3-notebook
aroot@lezo:~# pt-get remove python-pexpect python3-pexpect
root@lezo:~# pip3  install --upgrade pexpect
root@lezo:~# 
```

> Based on [Installing the Latest Python 3.7 on Ubuntu 16.04 | 18.04](https://websiteforstudents.com/installing-the-latest-python-3-7-on-ubuntu-16-04-18-04/)

### Check GPU can be used from python

To check that GPU can be used from python:

```
jadebustos@lezo:~$ cat gpu-example.py
# you need to install numpy, timeit and numba
import numpy as np
from timeit import default_timer as timer
from numba import vectorize
 
# This should be a substantially high value. On my test machine, this took
# 33 seconds to run via the CPU and just over 3 seconds on the GPU.
NUM_ELEMENTS = 100000000
 
# This is the CPU version.
def vector_add_cpu(a, b):
  c = np.zeros(NUM_ELEMENTS, dtype=np.float32)
  for i in range(NUM_ELEMENTS):
    c[i] = a[i] + b[i]
  return c
 
# This is the GPU version. Note the @vectorize decorator. This tells
# numba to turn this into a GPU vectorized function.
@vectorize(["float32(float32, float32)"], target='cuda')
def vector_add_gpu(a, b):
  return a + b;
 
def main():
  a_source = np.ones(NUM_ELEMENTS, dtype=np.float32)
  b_source = np.ones(NUM_ELEMENTS, dtype=np.float32)
 
  # Time the CPU function
  start = timer()
  vector_add_cpu(a_source, b_source)
  vector_add_cpu_time = timer() - start
 
  # Time the GPU function
  start = timer()
  vector_add_gpu(a_source, b_source)
  vector_add_gpu_time = timer() - start
 
  # Report times
  print("CPU function took %f seconds." % vector_add_cpu_time)
  print("GPU function took %f seconds." % vector_add_gpu_time)
 
  return 0
 
if __name__ == "__main__":
  main()
jadebustos@lezo:~$ python3 gpu-example.py 
CPU function took 55.155838 seconds.
GPU function took 0.751024 seconds.
jadebustos@lezo:~$ 
```

> [GPU Programming with Python](https://linuxhint.com/gpu-programming-python/)
