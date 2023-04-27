!deepspeed --num_gpus 4 \
    --module trainer \
    --input-model "EleutherAI/pythia-12b" \
    --deepspeed "configs/ds_config.json" \
    --epochs 2 \
    --local-output-dir "../models" \
    --dbfs-output-dir "../models" \
    --per-device-train-batch-size 6 \
    --per-device-eval-batch-size 6 \
    --logging-steps 10 \
    --save-steps 200 \
    --save-total-limit 20 \
    --eval-steps 50 \
    --warmup-steps 50 \
    --test-size 200 \
    --lr 5e-6
    --bf16 True
    --fp16 False


# for t4 GPUS

deepspeed --num_gpus 4 \
--module trainer \
--input-model "EleutherAI/pythia-6.9b" \
--deepspeed "configs/ds_t4_config.json" \
--epochs 2 \
--local-output-dir "../models" \
--dbfs-output-dir "../models" \
--per-device-train-batch-size 2 \
--per-device-eval-batch-size 2 \
--logging-steps 10 \
--save-steps 100 \
--save-total-limit 20 \
--eval-steps 100 \
--warmup-steps 20 \
--test-size 200 \
--lr 5e-6 \
--bf16 False \
--fp16 True



# this code will work only on cuda 11.7 with the pytorch version 
# link https://gist.github.com/primus852/b6bac167509e6f352efb8a462dcf1854

#!/bin/bash

### steps ####
# verify the system has a cuda-capable gpu
# download and install the nvidia cuda toolkit and cudnn
# setup environmental variables
# verify the installation
###

### to verify your gpu is cuda enable check
lspci | grep -i nvidia

### If you have previous installation remove it first. 
sudo apt-get purge nvidia*
sudo apt remove nvidia-*
sudo rm /etc/apt/sources.list.d/cuda*
sudo apt-get autoremove && sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*

# system update
sudo apt-get update
sudo apt-get upgrade

# install other import packages
sudo apt-get install g++ freeglut3-dev build-essential libx11-dev libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev

# first get the PPA repository driver
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update

# install nvidia driver with dependencies
sudo apt install libnvidia-common-530
sudo apt install libnvidia-gl-530
sudo apt install nvidia-driver-530

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /"
sudo apt-get update

 # installing CUDA-11.7
sudo apt install cuda-11-7 

# setup your paths
echo 'export PATH=/usr/local/cuda-11.7/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
sudo ldconfig

nvidia-smi 
nvcc -V


# seeting up the VM
sudo su 

sudo apt-get update
apt-get install wget
sudo apt-get install gcc



sudo apt install ubuntu-drivers-common
sudo apt install build-essential
sudo ubuntu-drivers autoinstall
sudo reboot

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
sudo apt-get update
sudo apt install cuda-11-7



nvidia-smi

wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
sha256sum Anaconda3-2022.05-Linux-x86_64.sh
bash Anaconda3-2022.05-Linux-x86_64.sh
source ~/.bashrc

conda create -n llm python=3.9
pip install -r req.txt



netstat -nlp | grep 80
kill -9 PID

find / -xdev -type f -size +102400000c

nvidia-smi 



# incase cuda and torch version does not match (10.1 and 11.7), to install 11.7
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
sudo apt-get update
sudo apt install cuda-11-7

# clone github repo

ssh-keygen -t rsa  # to generate rsa key to be pasted in azure devops
cat ~/.ssh/id_rsa.pub  # to print content in terminal 


git clone git@ssh.dev.azure.com:v3/MathCo-Innovation/Optimus/optimus-train