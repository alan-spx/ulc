# CV modules

## RAFT

**Install Anaconda**  
```
https://docs.anaconda.com/free/anaconda/install/linux/
```

**CUDA 10.1**  
```
https://medium.com/@exesse/cuda-10-1-installation-on-ubuntu-18-04-lts-d04f89287130
```

## OmniNeRF  

```
sudo apt install git  
```
```
mkdir src  
cd src  
git clone https://github.com/alan-spx/ulc  
git clone https://github.com/cyhsu14/OmniNeRF.git  
```
```
sudo apt update  
sudo apt remove --auto-remove nautilus  
```
```
sudo apt install python3.7
sudo apt install python3-pip
```

**.bashrc**  
```
alias python3=python3.7  
[ -d "$HOME/.local/bin" ] && PATH="$HOME/.local/bin:$PATH"  
export PATH  
```
```
python3 -V  
```
```
sudo apt install python3-pip  
python3.7 -m pip install pip  
pip3 -V  
python3.7 -m pip install --upgrade pip    
```
```
python3.7 -m pip install scikit-build  
python3.7 -m pip install -r requirements.txt  
```
```
python run_nerf.py --config configs/st3d.txt  
```

##  cuda 11.4  
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin  
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600  
wget https://developer.download.nvidia.com/compute/cuda/11.4.0/local_installers/cuda-repo-ubuntu1804-11-4-local_11.4.0-470.42.01-1_amd64.deb  
sudo dpkg -i cuda-repo-ubuntu1804-11-4-local_11.4.0-470.42.01-1_amd64.deb  
sudo apt-key add /var/cuda-repo-ubuntu1804-11-4-local/7fa2af80.pub  
sudo apt-get update  
sudo apt-get -y install cuda  
```

**.bashrc**  
```
export PATH="/usr/local/cuda-11.4/bin:$PATH"  
export LD_LIBRARY_PATH="/usr/local/cuda-11.4/lib64:$LD_LIBRARY_PATH"  
```
