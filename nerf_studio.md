## Homepage
```
https://docs.nerf.studio/index.html
https://github.com/nerfstudio-project/nerfstudio/
```

## Ubuntu 20.04
```
Ubuntu 20.04
```

## Change Kernel

[Change Kernel cuda.md](https://github.com/alan-spx/ulc/blob/master/cuda.md)  


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

# License
ENTER
q

# Do you accept the license terms?
yes

# /home/cv/anaconda3
ENTER
# wait ...

# Do you wish to update your shell profile to automatically initialize conda?
# [no] >>>
yes

source ~/.bashrc
conda list
```

### - Remove conda
```
conda remove -n ENV_NAME --all
```

## Python
```
python --version
# Python 3.11.7

conda create --name nerfstudio -y python=3.8

conda activate nerfstudio
# conda deactivate

pip install --upgrade pip
```

## Dependencies
```
pip install torch==2.1.2+cu118 torchvision==0.16.2+cu118 --extra-index-url https://download.pytorch.org/whl/cu118
conda install -c "nvidia/label/cuda-11.8.0" cuda-toolkit
pip install ninja git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch
```

## Installing nerfstudio
```
pip install nerfstudio
```

## Training
```
mkdir work
cd work

# Download some test data:
ns-download-data nerfstudio --capture-name=poster
# AssertionError: There is more than one folder inside this zip file: ['poster', '__MACOSX']
# Need to manually unzip data/nerfstudio/poster.zip

# Train model
ns-train nerfacto --data data/nerfstudio/poster
```

## Notes
```
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
╭─────────────── viser ───────────────╮
│             ╷                       │
│   HTTP      │ http://0.0.0.0:7007   │
│   Websocket │ ws://0.0.0.0:7007     │
│             ╵                       │
╰─────────────────────────────────────╯
[NOTE] Not running eval iterations since only viewer is enabled.
Use --vis {wandb, tensorboard, viewer+wandb, viewer+tensorboard} to run with eval.
No Nerfstudio checkpoint to load, so training from scratch.
Disabled comet/tensorboard/wandb event writers
[06:39:06] Printing max of 10 lines. Set flag --logging.local-writer.max-log-size=0 to disable line        writer.py:448
           wrapping. 
```
```

```
