## Command

```
rsync -vr from to    # copy files verbose and recursive

sudo date --set "29 Apr 2024 18:08:40"

mogrify -format jpg -- *  # save all images in the current folder to JPG format

```

## Tweaks - Change Ubuntu Themes

```
sudo apt install gnome-tweaks

## Change Themes
Appearance > Themes > Applications > Adwaita-dark

## Top Bar Weekday
Top Bar > Weekday
```

## Application icon location

```
/usr/share/pixmaps/meshlab.png
```

## Check library

```
pkg-config --cflags --libs opencv4
```

## Update Libreoffice Writer

```
https://ubuntuhandbook.org/index.php/2021/03/libreoffice-7-1-2-released-install-ubuntu-20-04-18-04/
```
```
https://ask.libreoffice.org/t/image-as-character-as-default/25152/5
```

## Alarm Clock

```
sudo add-apt-repository ppa:tatokis/alarm-clock-applet
sudo apt update
sudo apt install alarm-clock-applet
```

## Change background to solid color

```
gsettings set org.gnome.desktop.background picture-uri none
gsettings set org.gnome.desktop.background primary-color '#000000'
```

## Folders

```
/usr/include/opencv4/opencv2
/usr/include/pcl-1.10/pcl
```
```
/usr/lib/x86_64-linux-gnu/libopencv_core.so.4.2.0
/usr/lib/x86_64-linux-gnu/libpcl_io.so.1.10.0
```

## 22.04 disable TRASH icon on dock
```
sudo apt install -y dconf-editor
```
Search 'trash'

## New Fonts
**ms_fonts**
```
sudo mkdir /usr/local/share/fonts/ms_fonts

sudo mv ~/Downloads/*.ttc ~/Downloads/*.ttf /usr/local/share/fonts/ms_fonts/

sudo chown root:staff /usr/local/share/fonts/ms_fonts -R
sudo chmod 644 /usr/local/share/fonts/ms_fonts/* -R
sudo chmod 755 /usr/local/share/fonts/ms_fonts

sudo fc-cache -fv
```

## Personal installation

```
Ubuntu 22.04
OpenCV 4.5.5
```
### - Eigen
```
# eigen dependencies
sudo apt install -y gfortran

cd && cd src
wget -q https://gitlab.com/libeigen/eigen/-/archive/3.3.7/eigen-3.3.7.tar.bz2
tar xf eigen-3.3.7.tar.bz2 && rm -rf eigen-3.3.7.tar.bz2
cd eigen-3.3.7
mkdir -p build && cd build
cmake ..
make -j4
sudo make install
```
### - OpenCV 4.5.5
```
# OpenCV dependencies
sudo apt install -y libgtk-3-dev ffmpeg libavcodec-dev libavformat-dev libavutil-dev libswscale-dev libtbb-dev

cd && cd src
wget -q https://github.com/opencv/opencv/archive/4.5.5.zip
unzip -q 4.5.5.zip && rm -rf 4.5.5.zip

cd opencv-4.5.5
mkdir -p build && cd build

cmake ..
make -j4
sudo make install
```
```
python3 live_capture.py Error

pip3 install --upgrade pip
pip3 install opencv-contrib-python
```

## Keychron Linux Function Keys

```
sudo vim /etc/modprobe.d/hid_apple.conf
options hid_apple fnmode=2
sudo update-initramfs -u && reboot
```

```
https://www.reddit.com/r/Keychron/comments/lgotvh/keychron_k3_ubuntu_fn_keys/
```

## Ubuntu Common
```
Chrome keyring
- rm ~/.local/share/keyrings/*
- Now open Chrome; if it asks you for your password, do not enter one.
- Choose Continue each time and ignore any warnings.
```
```
KR CN input
sudo apt-get update
sudo apt-get install fcitx-googlepinyin
sudo apt-get install fcitx-hangul

Reboot

- Input Method Configuration > Global Config > Candidate Word Number: 10
https://hhddkk.wordpress.com/2016/06/02/install-google-pinyin-in-ubuntu-16-04/
https://m.blog.naver.com/opusk/220986268503
```

### - Shutdown button for Ubuntu dock
```
mkdir -p $HOME/.local/share/gnome-shell/extensions/KBD
touch $HOME/.local/share/gnome-shell/extensions/KBD/extension.js
touch $HOME/.local/share/gnome-shell/extensions/KBD/metadata.json
```
extension.js  
```
'use strict';

const St = imports.gi.St;

const Main = imports.ui.main;
const Util = imports.misc.util;

let button;

function _myKBD () {
Util.spawnCommandLine("bash /home/alan/.shutdown.sh")
}

function init() {
    button = new St.Bin({ style_class: 'panel-button',
                          reactive: true,
                          can_focus: true,
                          track_hover: true });
                          
    let icon = new St.Icon ({ icon_name: 'input-keyboard-symbolic',
                      style_class: 'system-status-icon' });
    button.set_child(icon);
    button.connect('button-press-event', _myKBD);
}

function enable() {
        Main.panel._rightBox.insert_child_at_index(button, 0);
}

function disable() {
        Main.panel._rightBox.remove_child(button);
}
```
metadata.json  
```
{
  "name": "KBD",
  "description": "KBD",
  "uuid": "KBD",
  "shell-version": [
    "3.36"
  ]
}
```
.shutdown.sh  
```
#!/bin/sh

echo wkddPwls | sudo -S shutdown now
```

```
Alt+F2 r Enter
gnome-extensions enable KBD
Alt+F2 r Enter
```

## LibreOffice Writer Dark Mode
```
Tools > Options > LibreOffice > Application Colors > General > Document background > Black
```

## Remmina
### - Server
```
Settings > Sharing > Screen Sharing >
- Allow connections to control the screen
- Require a password: ulc
- Wired connections 1
```
### - Client
```
Remmina
VNC > cv-NERF.local
ENTER
```

## 
