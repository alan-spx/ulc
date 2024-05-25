## Repo

```
https://github.com/ToniRV/NeRF-SLAM
```

## Install

```
Ubuntu 20.04
CUDA 11.8
```

```
Python 3.9
https://askubuntu.com/questions/1318846/how-do-i-install-python-3-9

ls -la /usr/bin/python3
sudo rm /usr/bin/python3
sudo ln -s python3.10 /usr/bin/python3
python3 --version

cd /usr/lib/python3/dist-packages
sudo cp apt_pkg.cpython-38-x86_64-linux-gnu.so apt_pkg.so

sudo apt install -y python3-pip

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
# Install open3d by the following first
python3 -m pip install --user open3d

pip install --no-index torch-scatter -f https://pytorch-geometric.com/whl/torch-2.0.0+cu118.html

pip install -r requirements.txt
pip install -r ./thirdparty/gtsam/python/requirements.txt

```
```
cmake version 3.29.3
apt remove cmake -y
pip install cmake --upgrade
sudo ln -s /home/cv/.local/bin/cmake /usr/bin/cmake 

cmake ./thirdparty/instant-ngp -B build_ngp
CUDACXX=/usr/local/cuda-11.8/bin/nvcc cmake ./thirdparty/instant-ngp -B build_ngp

```




