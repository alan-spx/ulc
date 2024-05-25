## Repo

```
https://github.com/ToniRV/NeRF-SLAM
```

## Install

```
Ubuntu 20.04

cmake version 3.29.3

CUDA 11.8

Python 3.9??

Python 3.10
https://gist.github.com/rutcreate/c0041e842f858ceb455b748809763ddb

cd /usr/lib/python3/dist-packages
sudo cp apt_pkg.cpython-38-x86_64-linux-gnu.so apt_pkg.so
curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10


Pytorch
pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118

```

Turn off the wired connection

```
git clone https://github.com/ToniRV/NeRF-SLAM.git --recurse-submodules
cd NeRF-SLAM
git submodule update --init --recursive
```

```
conda install pytorch==1.12.1 torchvision==0.13.1 torchaudio==0.12.1 cudatoolkit=11.3 -c pytorch



sudo apt install -y python3-pip

```


