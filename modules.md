# CV modules

## OpenVSLAM
```
Tested for Ubuntu 20.04.

# Dependencies

sudo apt update -y
sudo apt upgrade -y --no-install-recommends
sudo apt install -y build-essential pkg-config cmake git wget curl unzip libatlas-base-dev libsuitesparse-dev libgtk-3-dev ffmpeg libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev libtbb-dev gfortran binutils-dev libyaml-cpp-dev libgflags-dev sqlite3 libsqlite3-dev libglew-dev

# Eigen

cd ~/src
wget -q https://gitlab.com/libeigen/eigen/-/archive/3.3.7/eigen-3.3.7.tar.bz2
tar xf eigen-3.3.7.tar.bz2 && rm -rf eigen-3.3.7.tar.bz2
cd eigen-3.3.7
mkdir -p build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    ..
make -j4 && sudo make install

# OpenCV

cd ~/src
wget -q https://github.com/opencv/opencv/archive/4.5.5.zip
unzip -q 4.5.5.zip && rm -rf 4.5.5.zip
# Download aruco module (optional)
wget -q https://github.com/opencv/opencv_contrib/archive/refs/tags/4.5.5.zip -O opencv_contrib-4.5.5.zip
unzip -q opencv_contrib-4.5.5.zip && rm -rf opencv_contrib-4.5.5.zip
mkdir -p extra && mv opencv_contrib-4.5.5/modules/aruco extra
rm -rf opencv_contrib-4.5.5
# Build and install OpenCV
cd opencv-4.5.5
mkdir -p build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DBUILD_DOCS=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_JASPER=OFF \
    -DBUILD_OPENEXR=OFF \
    -DBUILD_PERF_TESTS=OFF \
    -DBUILD_TESTS=OFF \
    -DBUILD_PROTOBUF=OFF \
    -DBUILD_opencv_apps=OFF \
    -DBUILD_opencv_dnn=OFF \
    -DBUILD_opencv_ml=OFF \
    -DBUILD_opencv_python_bindings_generator=OFF \
    -DENABLE_CXX11=ON \
    -DENABLE_FAST_MATH=ON \
    -DWITH_EIGEN=ON \
    -DWITH_FFMPEG=ON \
    -DWITH_TBB=ON \
    -DWITH_OPENMP=ON \
    -DOPENCV_EXTRA_MODULES_PATH=/tmp/extra \
    ..
make -j4 && sudo make install

# FBoW 

cd ~/src
git clone https://github.com/stella-cv/FBoW.git
cd FBoW
mkdir build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    ..
make -j4 && sudo make install

# g2o.

cd ~/src
git clone https://github.com/RainerKuemmerle/g2o.git
cd g2o
git checkout 20230223_git
mkdir build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DBUILD_SHARED_LIBS=ON \
    -DBUILD_UNITTESTS=OFF \
    -DG2O_USE_CHOLMOD=OFF \
    -DG2O_USE_CSPARSE=ON \
    -DG2O_USE_OPENGL=OFF \
    -DG2O_USE_OPENMP=OFF \
    -DG2O_BUILD_APPS=OFF \
    -DG2O_BUILD_EXAMPLES=OFF \
    -DG2O_BUILD_LINKED_APPS=OFF \
    ..
make -j4 && sudo make install

# PangolinViewer

cd /tmp
git clone https://github.com/stevenlovegrove/Pangolin.git
cd Pangolin
git checkout eab3d3449a33a042b1ee7225e1b8b593b1b21e3e
mkdir build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_PANGOLIN_DEPTHSENSE=OFF \
    -DBUILD_PANGOLIN_FFMPEG=OFF \
    -DBUILD_PANGOLIN_LIBDC1394=OFF \
    -DBUILD_PANGOLIN_LIBJPEG=OFF \
    -DBUILD_PANGOLIN_LIBOPENEXR=OFF \
    -DBUILD_PANGOLIN_LIBPNG=OFF \
    -DBUILD_PANGOLIN_LIBTIFF=OFF \
    -DBUILD_PANGOLIN_LIBUVC=OFF \
    -DBUILD_PANGOLIN_LZ4=OFF \
    -DBUILD_PANGOLIN_OPENNI=OFF \
    -DBUILD_PANGOLIN_OPENNI2=OFF \
    -DBUILD_PANGOLIN_PLEORA=OFF \
    -DBUILD_PANGOLIN_PYTHON=OFF \
    -DBUILD_PANGOLIN_TELICAM=OFF \
    -DBUILD_PANGOLIN_UVC_MEDIAFOUNDATION=OFF \
    -DBUILD_PANGOLIN_V4L=OFF \
    -DBUILD_PANGOLIN_ZSTD=OFF \
    ..
make -j4 && sudo make install

```

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
