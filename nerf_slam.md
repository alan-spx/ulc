## Repo
```
https://github.com/ToniRV/NeRF-SLAM
```

## Ubuntu 20.04
```
Ubuntu 20.04
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

## Source Code
Turn off the wired connection

```
git clone https://github.com/ToniRV/NeRF-SLAM.git --recurse-submodules
cd NeRF-SLAM
git submodule update --init --recursive
```

## Python 3.9
```
# https://askubuntu.com/questions/1318846/how-do-i-install-python-3-9
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.9
python3.9 --version 
# Python 3.9.1+

sudo apt install python3.9-dev

ls -la /usr/bin/python3
sudo rm /usr/bin/python3
sudo ln -s python3.9 /usr/bin/python3
python3 --version

cd /usr/lib/python3/dist-packages
sudo cp apt_pkg.cpython-38-x86_64-linux-gnu.so apt_pkg.so

sudo apt install -y python3-pip
pip install --upgrade pip

# python is python3
# https://askubuntu.com/questions/320996/how-to-make-python-program-command-execute-python-3
```

## Python venv
```
sudo apt-get install python3.9-venv

cd
python3 -m venv venv

# https://stackoverflow.com/questions/64278198/error-can-not-perform-a-user-install-user-site-packages-are-not-visible-in
1. Go to the `pyvenv.cfg` file in the Virtual environment folder
2. Set the `include-system-site-packages` to `true` and save the change
3. Reactivate the virtual environment.

# Add to the end of ~/.bashrc
source venv/bin/activate

source ~/.bashrc

# deactivate
```

## Pytorch
```
pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118
```

## Open3D
```
# Install open3d by the following first
python3 -m pip install open3d
```

## Python requirements
```
pip install --no-index torch-scatter -f https://pytorch-geometric.com/whl/torch-2.0.0+cu118.html
pip install colored-glog

pip install -r requirements.txt
pip install -r ./thirdparty/gtsam/python/requirements.txt

```

## cmake
```
# cmake version 3.29.3
sudo apt remove cmake -y
pip install cmake --upgrade
sudo ln -s /home/cv/.local/bin/cmake /usr/bin/cmake 

# ~/.bashrc
export PATH="/usr/local/cuda/bin:$PATH"
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

## instant-ngp
```
sudo apt install -y xorg-dev libx11-dev libglew-dev

# NO -j for multi-thread

cd ./thirdparty/instant-ngp
cmake . -B build_ngp -DCMAKE_CUDA_COMPILER=$(which nvcc)
cmake --build build_ngp --config RelWithDebInfo -j6

# https://github.com/NVlabs/instant-ngp/issues/1142
```

## gtsam
```
sudo apt-get install -y libboost-all-dev libtbb-dev

# https://github.com/ToniRV/NeRF-SLAM/issues/7
# https://github.com/borglab/gtsam/issues/1298

# Build from source
# https://github.com/borglab/gtsam

git clone https://github.com/borglab/gtsam.git
cd gtsam

cmake . -DGTSAM_BUILD_PYTHON=1 -DGTSAM_PYTHON_VERSION=3.9.19 -B build_gtsam
cmake --build build_gtsam --config RelWithDebInfo -j6
cd build_gtsam
make python-install
```

## lietorch
```
# Failed in the first try
# https://askubuntu.com/questions/1268870/python-module-not-found-in-sudo-mode-ubuntu-20-04

cd ../../..
python setup.py install

```

## Sample Data
```
./scripts/download_replica_sample.bash

# cd to Datasets
# unzip replica_sample.zip

# move office0 to Replica
# move cam_params.json to Replica
```

## Change source code
```
# slam/vio_slam.py
-    naive_pose = gtsam.Pose3.identity()
+    naive_pose = gtsam.Pose3.Identity()

# slam/visual_frontends/visual_frontend.py
-    q = pose.rotation().quaternion()
-    return torch.tensor([t[0], t[1], t[2], q[1], q[2], q[3], q[0]], device=device, dtype=dtype)
+    q = pose.rotation().toQuaternion()
+    return torch.tensor([t[0], t[1], t[2], q.x(), q.y(), q.z(), q.w()], device=device, dtype=dtype) 
```

## Run
```
export PYTHONPATH=./thirdparty/instant-ngp/build_ngp/

cd ~/src/NeRF-SLAM
python ./examples/slam_demo.py --dataset_dir=./Datasets/Replica/office0 --dataset_name=nerf --buffer=100 --slam --parallel_run --img_stride=2 --fusion='sigma' --gui
```
