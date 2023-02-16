
## Get manual
```
sudo apt update
sudo apt install git
mkdir src
cd src
git clone https://github.com/alan-spx/ulc
sudo apt install ssh geany pcmanfm net-tools git gitk terminator  
```

## Unzip ZscalerRootCerts  
```
# Unzip ZscalerRootCerts
cd ZscalerRootCerts  
sudo mkdir /usr/local/share/ca-certificates/extra  
sudo cp ZscalerRootCertificate-2048-SHA256.crt /usr/local/share/ca-certificates/extra/root.cert.crt  
sudo update-ca-certificates  
cd
```

## Chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
sudo apt install ./google-chrome-stable_current_amd64.deb

gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'  
Power on
```

## New cmake
```
cd
sudo apt remove --purge --auto-remove cmake

sudo apt update && sudo apt install -y software-properties-common lsb-release && sudo apt clean all

wget -O - https://apt.kitware.com/keys/kitware-archive-latest.asc 2>/dev/null | gpg --dearmor - | sudo tee /etc/apt/trusted.gpg.d/kitware.gpg >/dev/null

sudo apt-add-repository "deb https://apt.kitware.com/ubuntu/ $(lsb_release -cs) main"

sudo apt update
sudo apt install kitware-archive-keyring
sudo rm /etc/apt/trusted.gpg.d/kitware.gpg

sudo apt update
sudo apt install cmake
cmake --version

sudo apt install build-essential libtool autoconf unzip wget
```

## CUDA


## Upgrade Python 3.6 to 3.7
```
python3 --version
sudo apt-get install python3.7
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
sudo update-alternatives --config python3
python3 -V
python -V

sudo apt-get install --reinstall python3-apt
cd /usr/lib/python3/dist-packages/
ls -l | grep apt_pkg
sudo ln -s apt_pkg.cpython-36m-x86_64-linux-gnu.so apt_pkg.so
```

## Build from source code
```
cd src/
git clone https://github.com/isl-org/Open3D
cd Open3D/
util/install_deps_ubuntu.sh
mkdir build
cd build
cmake ..
make -j$(nproc)
sudo make install

cd 
cd src/
git clone https://github.com/intel-isl/open3d-cmake-find-package.git
cd open3d-cmake-find-package
mkdir build
cd build
cmake ..
make -j
./Draw 
```

## Install open3d Python
```
sudo apt install python3-pip
pip3 install -U pip>=20.3

pip3 install cython
pip3 install numpy
pip3 install setuptools

pip3 install open3d

python3 -c "import open3d as o3d; print(o3d.__version__)"
python3 -c "import open3d as o3d; \
           mesh = o3d.geometry.TriangleMesh.create_sphere(); \
           mesh.compute_vertex_normals(); \
           o3d.visualization.draw(mesh, raw_mode=True)"
python3 -W default -c "import open3d as o3d"

sudo apt-get update
sudo apt install mesa-utils
sudo apt-get upgrade mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev

export MESA_GL_VERSION_OVERRIDE=4.5

glxinfo | grep "OpenGL version"

open3d example visualization/draw
```

