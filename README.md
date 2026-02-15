## Installing TensorFlow-GPU on Windows 11 with NVIDIA GeForce RTX 5060 by Anaconda

By Leo Cao | Version 1.0 | February 15, 2026

This articel describes how to install TensorFlow-GPU on Windows 11 with **NVIDIA GeForce RTX 5060** by Anaconda distribution.

### 0.Installation Environment
- **Hardware:**
    - **CPU:** Intel CORE Ultra 7
    - **Memory:** 32 GiB
    - **Disk:** 1 TiB NVMe SSD
    - **GPU:** NVIDIA GeForce RTX 5060

- **Software:**
  - **OS:** Windows 11 64-bit
  - **IDE:** Anaconda
  - **Language:** Python 3.7 (even though the Python version 3.7 is old, it is compatible with Tensorflow-GPU 2.4.0 on Windows 11)

### 1.Installation Preparation

Download the appropriate NVIDIA drivers from the official NVIDIA website (https://www.nvidia.com/en-us/drivers/), Generally, you should choose one of the following based on your primary use case:
- **GeForce Game Ready Driver:** OPtimized for the latest games.
- **NVIDIA Studio Driver:** Optimized for stability in creative and scienctific applications (often preferred for Deep Learning).
  
After intallation, verify the drivers are functioning properly using the `nvidia-smi` command in your terminal (COmmand Prompt):


```
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

### 2.TansorFlow-GPU Installation
```
conda create -n tf1 python-3.7
```
