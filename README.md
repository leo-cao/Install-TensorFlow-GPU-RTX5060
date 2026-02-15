# Installing TensorFlow-GPU on Windows 11 with NVIDIA GeForce RTX 5060 by Anaconda

> By Leo Cao | Version 1.0 | February 15, 2026

This article describes how to install TensorFlow-GPU on Windows 11 with **NVIDIA GeForce RTX 5060** by Anaconda distribution.

## 0. Installation Environment
- **Hardware:**
    - **CPU:** Intel CORE Ultra 7
    - **Memory:** 32 GiB
    - **Disk:** 1 TiB NVMe SSD
    - **GPU:** NVIDIA GeForce RTX 5060

- **Software:**
  - **OS:** Windows 11 64-bit
  - **IDE:** Anaconda
  - **Language:** Python 3.7 (even though the Python version 3.7 is old, it is compatible with Tensorflow-GPU 2.4.0 on Windows 11.)

## 1. Installation Preparation

### 1.1 Installing GPU Drivers

Download the appropriate NVIDIA drivers from the official [NVIDIA website](https://www.nvidia.com/en-us/drivers/), Generally, you should choose one of the following based on your primary use case:
- **GeForce Game Ready Driver:** Optimized for the latest games.
- **NVIDIA Studio Driver:** Optimized for stability in creative and scientific applications (often preferred for Deep Learning).
  
After installation, verify the drivers are functioning properly using the `nvidia-smi` command in your terminal (Command Prompt):


``` =
nvidia-smi
```

The output should display your GPU details and the supported CUDA version, similar to the information below:
```
WEEKDAY MONTH DAY HH:MM:SS YYYY
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 591.86                 Driver Version: 591.86         CUDA Version: 13.1     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                  Driver-Model | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 5060 ...  WDDM  |   00000000:02:00.0 Off |                  N/A |
| N/A   30C    P2             16W /   95W |       0MiB /   8151MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+
```

### 1.2 Installing Anaconda

Download Anaconda Distribution or Miniconda from official [Anaconda website](https://www.anaconda.com/download/), and install it.
Verify conda works correctly using the `conda --version` command in your **Anaconda PowerShell Prompt** or **Anaconda Prompt**.
``` =
conda --version
```

The output should display you conda version, similar to the information below:
```
conda 26.1.0
```


## 2. TensorFlow-GPU Installation

### 2.1 Check TensorFlow Capability 

Before proceeding, verify tested build configurations on official [TensorFlow website](https://www.tensorflow.org/install/source_windows). For this setup, we are installing`tensorflow_gpu==2.4.0`.

|Version | Python version | Compiler | Build tools | cuDNN | CUDA |
| :---: | :---: | :---: | :---: | :---: | :---: |
|**tensorflow_gpu-2.4.0** |	3.6-3.8 |	MSVC 2019 |	Bazel 3.1.0 |	8.0	 | 11.0 |
| | | | | |


### 2.2 Create a Virtual Environment with Anaconda

Create a virtual environment named `tf2` using the `conda' command in your **Anaconda PowerShell Prompt** or **Anaconda Prompt**.

```= 
conda create -n tf2 python=3.7
```

When prompted, press `y` with `ENTER` to proceed.
```Plaintext
Proceed ([y]/n)? y
```
To activate the new environment, run:

``` =
conda activate tf2
```

### 2.3 Install CUDA Toolkit

Search for the `cudatoolkit` version in the `conda-forge` channel:
```=
conda search cudatoolkit -c conda-forge 
```

You should see `cudatoolkit 11.0.221` (or similar) in the results:
```Plaintext
# Name                       Version           Build  Channel
cudatoolkit                 11.0.221      h74a9793_0  pkgs/main
``` 

Install the toolkit using the following command:
``` =
conda install cudatoolkit=11.0.221 -c conda-forge 
```


### 2.4 Install `cuDNN`

Next, search for a compatible `cudnn` version. Version **8.0.5.39** should be available.
```
conda search cudnn -c conda-forge 
```

Install it using:
``` =
conda install cudnn= 8.0.5.39 -c conda-forge 
```

### 2.5 Install `TensorFlow-GPU`

Install the specific TensorFlow wheel file using `pip`.
> **Note:** This example is an Aliyn mirror for faster download speeds in certain regions.

``` =
pip install https://mirrors.aliyun.com/pypi/packages/ea/9a/68f5b2dad5293a505d7d66f47ee9be4061fff0b88511aa5a1b38941a12d5/tensorflow_gpu-2.4.0-cp37-cp37m-win_amd64.whl
```

## 3. Verification

First, verify that the installed versions of `cudatoolkit`, `cudnn` and `tensorflow_gpu` align with the requirements in Step 2.1:
```
conda list
```

Then, verify GPU visibility within Python in the virtual environment `tf2`:
``` =
conda activate tf2
```
``` = 
python
```

Run the following script:
```Python =
import tensorflow as tf
tf.test.gpu_device_name()
```

The output should confirm the **NVIDIA GeForce RTX 5060**, appearing similar to this:

```Plaintext 
Successfully opened dynamic library cudart64_110.dll
pciBusID: 0000:02:00.0 name: NVIDIA GeForce RTX 5060 computeCapability: 12.0
```
