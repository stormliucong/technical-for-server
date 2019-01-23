
## install cuda on ubuntu_16.04

### 1. install nvidia graphic driver
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-390
sudo reboot
#### test to see wether it succeeded
nvidia-smi
```
```
Wed Jan 23 17:05:09 2019
`+-----------------------------------------------------------------------------+
| NVIDIA-SMI 390.87                 Driver Version: 390.87                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  TITAN Xp            Off  | 00000000:3B:00.0 Off |                  N/A |
| 23%   37C    P0    61W / 250W |      0MiB / 12196MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   1  TITAN Xp            Off  | 00000000:5E:00.0 Off |                  N/A |
| 23%   27C    P0    59W / 250W |      0MiB / 12196MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   2  TITAN Xp            Off  | 00000000:86:00.0 Off |                  N/A |
| 23%   27C    P0    61W / 250W |      0MiB / 12196MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   3  TITAN Xp            Off  | 00000000:AF:00.0 Off |                  N/A |
| 23%   29C    P0    56W / 250W |      0MiB / 12196MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+ 
```
#### trouble shooting
```
NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.
```
reboot without security just 
```
sudo reboot
```

# 2. install cuda 9.0
```
# change the link if can not be found.
sudo wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux.run
sudo chmod +x cuda_9.0.176_384.81_linux.run
sudo ./cuda_9.0.176_384.81_linux.run --override
# Answer questions following while installation begin
# yes except for Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 384.81? is No
vi /etc/environment
# add PATH=/usr/local/cuda-9.0/bin:$PATH
# add LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH
sudo reboot
```

# 3. install cudnn 7.0, which support for cuda 9.0
```
# register before downloading.
tar -xzvf ${CUDNN_TAR_FILE}
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-9.0/include
sudo cp -P cuda/lib64/libcudnn* /usr/local/cuda-9.0/lib64/
sudo chmod a+r /usr/local/cuda-9.0/lib64/libcudnn*
```
