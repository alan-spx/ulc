# ULC

## URL
```
[]()  
```

## Steps
```
- Ubuntu 20.04
- Basic install
- git clone ulc
- Chrome, security
- ROS
- CUDA 11.8
- Pytorch
- high-res-stereo
- OpenCV *.*
- OpenVSLAM
```

## Boot
NUC: F10 -> UEFI, F2 -> BIOS  
ThinkPad: F12 -> Boot
```
Power -> Secondary Power Settings -> After Power Failure -> Power On  
```

## git
```
sudo apt install -y git gitk geany
mkdir src  
cd src  
git clone https://github.com/alan-spx/ulc

cd ulc
gedit ./README.md
```

## Power on
```
power never  
dconf write /org/gnome/desktop/interface/clock-show-date 'true'
gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'  
```

## sudo
```
sudo apt-get remove --auto-remove -y nautilus  
sudo apt update  
sudo apt install -y ssh pcmanfm net-tools terminator cmake build-essential

sudo apt-get install xfce4-terminal
```

## ZscalerRootCerts
```
cd ~/src/ulc
unzip -q ZscalerRootCerts.zip && rm ZscalerRootCerts.zip
cd ZscalerRootCerts  
sudo mkdir /usr/local/share/ca-certificates/extra  
sudo cp ZscalerRootCertificate-2048-SHA256.crt /usr/local/share/ca-certificates/extra/root.cert.crt  
sudo update-ca-certificates  
cd
```

## Chrome
```
cd  
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb  
sudo apt install -y ./google-chrome-stable_current_amd64.deb
```

Chrome settings:  
```
Security --> Manage certificates --> Authorities --> Import  
```

## New cmake
```
https://askubuntu.com/questions/355565/how-do-i-install-the-latest-version-of-cmake-from-the-command-line  
Run A1~A6
```

## Upgrade Python 3.6 to 3.7
```
https://www.itsupportwale.com/blog/how-to-upgrade-to-python-3-7-on-ubuntu-18-10/  
```

## Terminator won't open
```
By any means (knowingly or unknowingly) you must have downgraded the python version in your ubuntu for which you are facing such problem :)
https://www.reddit.com/r/Ubuntu/comments/yn9w37/i_cant_open_the_terminal_please_help/
```

## Terminal Alternatives
```
- Visual Studio Code -> Terminal -> New Terminal
- 
```

## ROS  
https://wiki.ros.org/noetic/Installation/Ubuntu

```
mkdir -p ~/catkin_ws/src  
cd ~/catkin_ws/  
catkin_make
```

## Apriltag  
```
git clone https://github.com/AprilRobotics/apriltag  
cd apriltag  
mkdir build  
cd build  
cmake ..  
make -j  
sudo make install
```

## TIS  
```
git clone https://github.com/TheImagingSource/tiscamera    
cd tiscamera  
git checkout baacb4cfaa7858c2e6cfb4f1a297b404c4e002f6  
./scripts/dependency-manager install  
mkdir build  
cd build  
cmake -DBUILD_ARAVIS=ON ..  
make -j  
sudo make install  
```

Link-Local Only

two-cams Git version
```
git checkout cd7947e2
* cd7947e2 2022-12-22 | src: fix LibraryHandlenamespace (#502) (HEAD -> master, origin/master, origin/HEAD) [xiliugatech]
```

**tcam-gigetool**  
```
https://www.theimagingsource.com/documentation/tiscamera/tcam-gigetool.html  
tcam-gigetool list  
tcam-gigetool info ####  
tcam-gigetool set --mode dhcp ####  
tcam-gigetool set --mode static ####  
```

**GX183 stereo network setting**  
```
Link-Local Only
```

**Tiscamera Camera Library**  
```
https://www.theimagingsource.com/en-us/support/download/tiscamera1804-1.1.0.4139/
```

**Tiscamera Development Package**  
```
https://www.theimagingsource.com/en-de/support/download/tiscameratiscameradev-1.1.0.4139/  
```

**Save an image using OpenCV**  
```
https://github.com/TheImagingSource/Linux-tiscamera-Programming-Samples/tree/master/cpp/Save%20an%20image%20using%20OpenCV  
```


## Pangolin
```
sudo apt install -y libglew-dev  
```

```
cd ~/src  
git clone https://github.com/stevenlovegrove/Pangolin.git  
cd Pangolin  
git checkout ad8b5f83222291c51b4800d5a5873b0e90a0cf81  
mkdir build && cd build  
cmake \  
    -DCMAKE_BUILD_TYPE=Release \  
    -DCMAKE_INSTALL_PREFIX=/usr/local \  
    ..  
make -j4  
sudo make install  
```

## vision_msgs
```
cd ~/catkin_ws/src/ && git clone https://github.com/ros-perception/vision_msgs.git  
```

## Velodyne
http://wiki.ros.org/velodyne/Tutorials/Getting%20Started%20with%20the%20Velodyne%20VLP16  

static IP  
```
sudo apt-get install -y ros-melodic-velodyne  
cd ~/catkin_ws/src/ && git clone https://github.com/ros-drivers/velodyne.git  
cd ..  
rosdep install --from-paths src --ignore-src --rosdistro melodic -y  
catkin_make
```

```
roslaunch velodyne_pointcloud VLP16_points.launch  
rosrun rviz rviz -f velodyne  
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map velodyne 10  
```

default velodyne IP: 192.168.1.201  

## Velodyne dual  

**Dual Lidar**  "hgrw commented on May 7, 2019"  
https://github.com/ros-drivers/velodyne/issues/108

```
roslaunch velodyne_pointcloud VLP16_dual.launch  
rviz rviz  
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp201 10  
rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map vlp202 10  
```

## Ouster
firefox: os-122218000386.local  
```
roslaunch ouster_ros ouster.launch sensor_hostname:=169.254.165.155 metadata:=/home/cv/metadata.json  
rviz rviz -f os_lidar  
rosbag record -a
```

## .bashrc
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc  
echo "source /home/**user_name**/catkin_ws/devel/setup.bash" >> ~/.bashrc  
source ~/.bashrc
```

## Memo

https://static.ouster.dev/sensor-docs/image_route1/image_route2/common_sections/API/tcp-api.html  

Would you be able to run the following command utilizing the TCP API and send me the results:  
nc 122218000386.local 7501  
get_telemetry  

## .gitconfig

[user]  
        name = A Zhang  
        email = akcite@gmail.com  
	name = Alan Zhang  
        email = guoxuan.zhang@spx.com  
[alias]  
        acm = !git add -A && git commit -m  
        co = checkout  
        ci = commit  
        st = status  
        br = branch  
        hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short  
        type = cat-file -t  
        dump = cat-file -p  
        rh = reset --hard  
        ls-repo = !git ls-tree --full-tree -r HEAD  

## image_view

```
roslaunch tcam_publish tcam_publish.launch cam_name:=cam_front cam_serial:=#38810013  
rosrun image_view image_view image:=/cam_front_publish/image_rect  
```
(mouse right click, save to current folder)  

shorturl.at/ANO37


## TeamViewer
https://www.teamviewer.com/en/download/linux  
```
sudo apt install -y ./teamviewer_15.32.3_amd64.deb 
```


## Sharing
```
ssh cv-NUC10i7FNK.local
```


## Vision_msg

[12:33 PM] Artes, Benjamin  
I'd like for you to use the vision_msgs/BoundingBox3DArray message that's part of the vision_msgs package for LIDAR. If no objects are present leave the array empty.

To install this package `sudo apt install -y ros-melodic-vision-msgs`  
vision_msgs/BoundingBox3DArray Documentation

[12:34 PM] Artes, Benjamin  
(pose.position should be the position you're using, and pose.orientation should be identity (x: 0, y: 0, z: 0, w: 1)

[12:35 PM] Artes, Benjamin  
And please fill out the header.frame_id with the name of the lidar (front_lidar or back_lidar)


## IP settings

**CV: Solar robot**

Address: 192.168.0.1  
Netmask: 255.255.255.0  
Gateway: 192.168.0.1  

**CV: Personal use**

Address: 192.168.1.1  
Netmask: 255.255.255.0  
Gateway: N/A

**Velodyne Lidar**  


## ceres-solver 

```
sudo apt-get install -y cmake  
sudo apt-get install -y libgoogle-glog-dev libgflags-dev  
sudo apt-get install -y libatlas-base-dev  
sudo apt-get install -y libeigen3-dev  
sudo apt-get install -y libsuitesparse-dev  
```

```
cd && cd src  
wget http://ceres-solver.org/ceres-solver-2.1.0.tar.gz  
tar zxf ceres-solver-2.1.0.tar.gz  
mkdir ceres-bin  
cd ceres-bin  
cmake ../ceres-solver-2.1.0  
make -j  
make test  
sudo make install  
bin/simple_bundle_adjuster ../ceres-solver-2.1.0/data/problem-16-22106-pre.txt  
```


## spdlog

```
git clone https://github.com/gabime/spdlog.git  
cd spdlog && mkdir build && cd build  
cmake .. && make -j  
sudo make install  
```

## clang-format

```
sudo apt install -y clang-format  
find src/ -iname *.h -o -iname *.cpp | xargs clang-format -i  
```
```
clang-format -i -style=llvm src/csv_to_text.cpp 
```

## OpenCV

From stella_vslam  

**Dependencies**  
```
sudo apt install -y libgtk-3-dev  
sudo apt install -y ffmpeg  
sudo apt install -y libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libavresample-dev  
```

**Install**
```
cd /path/to/working/dir
wget https://github.com/opencv/opencv/archive/3.4.0.zip
unzip -q 3.4.0.zip
rm -rf 3.4.0.zip
cd opencv-3.4.0
mkdir -p build && cd build
cmake \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr/local \
    -DENABLE_CXX11=ON \
    -DBUILD_DOCS=OFF \
    -DBUILD_EXAMPLES=OFF \
    -DBUILD_JASPER=OFF \
    -DBUILD_OPENEXR=OFF \
    -DBUILD_PERF_TESTS=OFF \
    -DBUILD_TESTS=OFF \
    -DWITH_EIGEN=ON \
    -DWITH_FFMPEG=ON \
    -DWITH_OPENMP=ON \
    ..
make -j4
sudo make install
```

## Geany
```
Change Color Scheme
Theme: InkPot

wget https://raw.github.com/geany/geany-themes/master/colorschemes/inkpot.conf

Download to  
~/.config/geany/colorschemes/inkpot.conf  
In Geany  
View/Change Color Scheme  

https://github.com/geany/geany-themes  
https://www.geany.org/download/themes/
```
### - Underscore
```
Tools > Configuration Files > filetypes.common

[styling]
line_height=0;2;
```

## Ubuntu Icon Entry
```
[Desktop Entry]
Name=Eclipse
Type=Application
Exec=/home/USERNAME/java-mars/eclipse/eclipse
Terminal=false
Icon=/home/USERNAME/java-mars/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE;
Name[en]=Eclipse

https://ubuntuhandbook.org/index.php/2016/01/how-to-install-the-latest-eclipse-in-ubuntu-16-04-15-10/
```

## Repo
```
https://github.com/ULC-Robotics/apriltag_localization
https://github.com/ULC-Robotics/cross_localization
```

## Install OpenCL
```
sudo apt update
sudo apt install ocl-icd-opencl-dev
```


