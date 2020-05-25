# Gigabyte GT 1030

+ [Gigabyte GT 1030 Low Profile D4 2G Specs](https://www.cnet.com/products/gigabyte-gt-1030-low-profile-d4-2g-graphics-card-gf-gt-1030-2-gb/)
+ [GIGABYTE GT 1030 Low Profile](https://www.techpowerup.com/gpu-specs/gigabyte-gt-1030-low-profile.b4616)
+ [CUDA Toolkit 8.0 - Feb 2017](https://developer.nvidia.com/cuda-80-ga2-download-archive)

# Installing Cuda on Ubuntu 16.04

Install the CUDA toolkit without the drivers:

```
root@lezo:~# wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run
root@lezo:~# chmod +x cuda_8.0.61_375.26_linux-run
root@lezo:~# ./cuda_8.0.61_375.26_linux-run --silent --toolkit --samples
root@lezo:~#
```

Install drivers:

```
root@lezo:~# add-apt-repository -y ppa:graphics-drivers/ppa
root@lezo:~# apt update
root@lezo:~# apt install nvidia-418 nvidia-418-dev libcuda1-418 nvidia-opencl-icd-418
root@lezo:~#
```

Check that all is working properly:

```
root@lezo:~# nvidia-smi 
Mon May 25 22:28:07 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 418.56       Driver Version: 418.56       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GT 1030     Off  | 00000000:03:00.0 Off |                  N/A |
|  0%   42C    P0    N/A /  30W |    415MiB /  2001MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      8574      C   /usr/bin/python3                             413MiB |
+-----------------------------------------------------------------------------+
root@lezo:~# 
```

Apply cuda patch:

```
root@lezo:~# wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/patches/2/cuda_8.0.61.2_linux-run
root@lezo:~# chmod +x cuda_8.0.61.2_linux-run
root@lezo:~# ./cuda_8.0.61.2_linux-run 
root@lezo:~# nvidia-smi
Mon May 25 22:31:06 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 418.56       Driver Version: 418.56       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GT 1030     Off  | 00000000:03:00.0 Off |                  N/A |
|  0%   42C    P0    N/A /  30W |    415MiB /  2001MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      8574      C   /usr/bin/python3                             413MiB |
+-----------------------------------------------------------------------------+
root@lezo:~#
```

Let's check the device:

```
root@lezo:~# cd NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery
root@lezo:~/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery# make
root@lezo:~/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery# ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GT 1030"
  CUDA Driver Version / Runtime Version          10.1 / 8.0
  CUDA Capability Major/Minor version number:    6.1
  Total amount of global memory:                 2001 MBytes (2098528256 bytes)
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
  Run time limit on kernels:                     No
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 3 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 10.1, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = GeForce GT 1030
Result = PASS
root@lezo:~/NVIDIA_CUDA-8.0_Samples/1_Utilities/deviceQuery# 
```

Add the following to your **.bashrc** or **.bash_profile**:

```
PATH=$PATH:/usr/local/cuda-8.0/bin
```

> Based on [Using the nVidia GT 1030 for CUDA workloads on Ubuntu 16.04](https://medium.com/@samnco/using-the-nvidia-gt-1030-for-cuda-workloads-on-ubuntu-16-04-4eee72d56791)

## Troubleshouting

Verify that the nvidia-settings package matches your driver version:

```
root@lezo:~# dpkg -l | grep nvidia-settings
ii  nvidia-settings                                   418.56-0ubuntu0~gpu16.04.1                      amd64        Tool for configuring the NVIDIA graphics driver
root@lezo:~# 
```

# Installing python3 and jupyter notebook on Ubuntu 16.04

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

## Check GPU can be used from python

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