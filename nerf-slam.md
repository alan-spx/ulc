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
# https://askubuntu.com/questions/1318846/how-do-i-install-python-3-9

sudo apt install python3.9-dev

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
sudo apt remove cmake -y
pip install cmake --upgrade
sudo ln -s /home/cv/.local/bin/cmake /usr/bin/cmake 

export PATH="/usr/local/cuda/bin:$PATH"
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

```
sudo apt install -y xorg-dev libx11-dev
sudo apt install libglew-dev

# NO -j for multi-thread

cd ./thirdparty/instant-ngp
cmake . -B build_ngp
cmake --build build_ngp --config RelWithDebInfo 

# https://github.com/NVlabs/instant-ngp/issues/1142
```

```
sudo apt-get install libboost-all-dev libtbb-dev

# https://github.com/ToniRV/NeRF-SLAM/issues/7
# Build from source
# https://github.com/borglab/gtsam
mkdir build
cd build
cmake ..
make check (optional, runs unit tests)
sudo make install

# https://github.com/borglab/gtsam/tree/develop/python
cd ..
pip install -r python/dev_requirements.txt
cd build
cmake .. -DGTSAM_BUILD_PYTHON=1 -DGTSAM_PYTHON_VERSION=3.9.19
make -j6


```




