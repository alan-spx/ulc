## Homepage
```
https://docs.nerf.studio/index.html
https://github.com/nerfstudio-project/nerfstudio/
```

## Ubuntu 20.04
```
Ubuntu 20.04
```

## CUDA Docs
```
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html
```


## Commands
```
lsb_release -a    # Ubuntu version
uname -r          # kernel version
gcc -v            # GCC version
ldd --version     # GLIBC version
```


## Change Kernel
```
sudo grub-mkconfig | grep -iE "menuentry 'Ubuntu, with Linux" | awk '{print i++ " : "$1, $2, $3, $4, $5, $6, $7}'
uname -srn
sudo geany /etc/default/grub

# Quote mark matters

GRUB_DEFAULT="1>2"
sudo update-grub
sudo systemctl reboot
```

```
https://askubuntu.com/questions/82140/how-can-i-boot-with-an-older-kernel-version
# Answered by Namasivayam Chinnapillai
```


## CUDA 11.8
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```

## Conda

```
# https://www.anaconda.com/download/
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh
```

```
cd ~/Downloads
chmod +x Anaconda3-20**.**-Linux-x86_64.sh
./Anaconda3-20**.**-Linux-x86_64.sh

q
yes
ENTER
yes

source ~/.bashrc
conda list
```

```
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.4 -c pytorch -c nvidia
```

