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
Step (% Done)       Vis Rays / Sec       Train Iter (time)    ETA (time)           Train Rays / Sec      
-------------------------------------------------------------------------------------------------------- 
29910 (99.70%)      101.070 ms           9 s, 96.299 ms       41.18 K                                    
29920 (99.73%)      101.655 ms           8 s, 132.408 ms      41.04 K                                    
29930 (99.77%)      102.165 ms           7 s, 151.529 ms      41.09 K                                    
29940 (99.80%)      99.065 ms            5 s, 943.906 ms      42.15 K                                    
29950 (99.83%)      97.951 ms            4 s, 897.541 ms      42.59 K                                    
29960 (99.87%)      100.309 ms           4 s, 12.370 ms       41.77 K                                    
29970 (99.90%)      99.159 ms            2 s, 974.759 ms      42.04 K                                    
29980 (99.93%)      98.287 ms            1 s, 965.749 ms      42.43 K                                    
29990 (99.97%)      100.554 ms           1 s, 5.535 ms        41.72 K                                    
29999 (100.00%)                                                                                          
----------------------------------------------------------------------------------------------------     
Viewer running locally at: http://localhost:7007 (listening on 0.0.0.0)                                  
╭─────────────────────────────── 🎉 Training Finished 🎉 ────────────────────────────────╮
│                        ╷                                                               │
│   Config File          │ outputs/poster/nerfacto/2024-05-29_064436/config.yml          │
│   Checkpoint Directory │ outputs/poster/nerfacto/2024-05-29_064436/nerfstudio_models   │
│                        ╵                                                               │
╰────────────────────────────────────────────────────────────────────────────────────────╯
                                                   Use ctrl+c to quit                                                

```
```
(nerfstudio) cv@cv-NERF:~/work$ ns-export poisson --load-config outputs/poster/nerfacto/2024-05-28_214755/config.yml --output-dir exports/mesh/ --target-num-faces 50000 --num-pixels-per-side 2048 --num-points 1000000 --remove-outliers True --normal-method open3d 
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.11/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

[22:45:56] Auto image downscale factor of 2                                                 nerfstudio_dataparser.py:484
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.11/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

Started threads
Setting up evaluation dataset...
Caching all 22 images.
Loading data batch ━━━━━━━━━━━━━━━━━━━━━━━━━━━━╺━━━━━━━━━━━  71% 0:00:01tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
Loading data batch ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:02
Loading latest checkpoint from load_dir
✅ Done loading checkpoint from outputs/poster/nerfacto/2024-05-28_214755/nerfstudio_models/step-000029999.ckpt
☁ Computing Point Cloud ☁ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 00:13
✅ Cleaning Point Cloud
✅ Estimating Point Cloud Normals
✅ Generated PointCloud with 1001931 points.
✅ Computing Mesh this may take a while.
✅ Saving Mesh
Running meshing decimation with quadric edge collapse
Texturing mesh with NeRF
Unwrapping mesh with xatlas method... this may take a while.
✅ Unwrapped mesh with xatlas method━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 02:34
Creating texture image by rendering with NeRF...
Writing relevant OBJ information to files...
Writing vertices to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing vertices to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing vertex normals to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing faces to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 165198.02 lines-per-sec 00:00
────────────────────────────────────────────── 🎉 🎉 🎉 All DONE 🎉 🎉 🎉 ──────────────────────────────────────────────
                                          Unwrapped mesh using xatlas method.                                           
                                        Mesh has 24195 vertices and 50000 faces.                                        
                         Length of rendered rays to compute texture values: 6.4665398597717285                          
                                        OBJ file saved to exports/mesh/mesh.obj                                         
                                     MTL file saved to exports/mesh/material_0.mtl                                      
                   Texture image saved to exports/mesh/material_0.png with resolution 2048x2048 (WxH)                   
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
(nerfstudio) cv@cv-NERF:~/work$ 
```
