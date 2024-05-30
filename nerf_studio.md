## Homepage
```
[NerfStudio Homepage](https://docs.nerf.studio/index.html)
[NerfStudio Github](https://github.com/nerfstudio-project/nerfstudio/)
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

### - Python
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

## Export
```
# Point Cloud
ns-export pointcloud --load-config outputs/poster/nerfacto/2024-05-29_064436/config.yml --output-dir exports/pcd/ --num-points 1000000 --remove-outliers True --normal-method open3d --save-world-frame False

# Mesh
ns-export poisson --load-config outputs/poster/nerfacto/2024-05-29_064436/config.yml --output-dir exports/mesh/ --target-num-faces 50000 --num-pixels-per-side 2048 --num-points 1000000 --remove-outliers True --normal-method open3d
```

## Logs

### - Train
```
(nerfstudio) cv@cv-NERF:~/temp$ ns-train nerfacto --data data/nerfstudio/poster
[07:49:21] Using --data alias for --data.pipeline.datamanager.data                                          train.py:230
──────────────────────────────────────────────────────── Config ────────────────────────────────────────────────────────
TrainerConfig(
    _target=<class 'nerfstudio.engine.trainer.Trainer'>,
    output_dir=PosixPath('outputs'),
    method_name='nerfacto',
    experiment_name=None,
    project_name='nerfstudio-project',
    timestamp='2024-05-29_074921',
    machine=MachineConfig(seed=42, num_devices=1, num_machines=1, machine_rank=0, dist_url='auto', device_type='cuda'),
    logging=LoggingConfig(
        relative_log_dir=PosixPath('.'),
        steps_per_log=10,
        max_buffer_size=20,
        local_writer=LocalWriterConfig(
            _target=<class 'nerfstudio.utils.writer.LocalWriter'>,
            enable=True,
            stats_to_track=(
                <EventName.ITER_TRAIN_TIME: 'Train Iter (time)'>,
                <EventName.TRAIN_RAYS_PER_SEC: 'Train Rays / Sec'>,
                <EventName.CURR_TEST_PSNR: 'Test PSNR'>,
                <EventName.VIS_RAYS_PER_SEC: 'Vis Rays / Sec'>,
                <EventName.TEST_RAYS_PER_SEC: 'Test Rays / Sec'>,
                <EventName.ETA: 'ETA (time)'>
            ),
            max_log_size=10
        ),
        profiler='basic'
    ),
    viewer=ViewerConfig(
        relative_log_filename='viewer_log_filename.txt',
        websocket_port=None,
        websocket_port_default=7007,
        websocket_host='0.0.0.0',
        num_rays_per_chunk=32768,
        max_num_display_images=512,
        quit_on_train_completion=False,
        image_format='jpeg',
        jpeg_quality=75,
        make_share_url=False,
        camera_frustum_scale=0.1,
        default_composite_depth=True
    ),
    pipeline=VanillaPipelineConfig(
        _target=<class 'nerfstudio.pipelines.base_pipeline.VanillaPipeline'>,
        datamanager=ParallelDataManagerConfig(
            _target=<class 'nerfstudio.data.datamanagers.parallel_datamanager.ParallelDataManager'>,
            data=PosixPath('data/nerfstudio/poster'),
            masks_on_gpu=False,
            images_on_gpu=False,
            dataparser=NerfstudioDataParserConfig(
                _target=<class 'nerfstudio.data.dataparsers.nerfstudio_dataparser.Nerfstudio'>,
                data=PosixPath('.'),
                scale_factor=1.0,
                downscale_factor=None,
                scene_scale=1.0,
                orientation_method='up',
                center_method='poses',
                auto_scale_poses=True,
                eval_mode='fraction',
                train_split_fraction=0.9,
                eval_interval=8,
                depth_unit_scale_factor=0.001,
                mask_color=None,
                load_3D_points=False
            ),
            train_num_rays_per_batch=4096,
            train_num_images_to_sample_from=-1,
            train_num_times_to_repeat_images=-1,
            eval_num_rays_per_batch=4096,
            eval_num_images_to_sample_from=-1,
            eval_num_times_to_repeat_images=-1,
            eval_image_indices=(0,),
            collate_fn=<function nerfstudio_collate at 0x7f7fcbdff0d0>,
            camera_res_scale_factor=1.0,
            patch_size=1,
            camera_optimizer=None,
            pixel_sampler=PixelSamplerConfig(
                _target=<class 'nerfstudio.data.pixel_samplers.PixelSampler'>,
                num_rays_per_batch=4096,
                keep_full_image=False,
                is_equirectangular=False,
                ignore_mask=False,
                fisheye_crop_radius=None,
                rejection_sample_mask=True,
                max_num_iterations=100
            ),
            num_processes=1,
            queue_size=2,
            max_thread_workers=None
        ),
        model=NerfactoModelConfig(
            _target=<class 'nerfstudio.models.nerfacto.NerfactoModel'>,
            enable_collider=True,
            collider_params={'near_plane': 2.0, 'far_plane': 6.0},
            loss_coefficients={'rgb_loss_coarse': 1.0, 'rgb_loss_fine': 1.0},
            eval_num_rays_per_chunk=32768,
            prompt=None,
            near_plane=0.05,
            far_plane=1000.0,
            background_color='last_sample',
            hidden_dim=64,
            hidden_dim_color=64,
            hidden_dim_transient=64,
            num_levels=16,
            base_res=16,
            max_res=2048,
            log2_hashmap_size=19,
            features_per_level=2,
            num_proposal_samples_per_ray=(256, 96),
            num_nerf_samples_per_ray=48,
            proposal_update_every=5,
            proposal_warmup=5000,
            num_proposal_iterations=2,
            use_same_proposal_network=False,
            proposal_net_args_list=[
                {'hidden_dim': 16, 'log2_hashmap_size': 17, 'num_levels': 5, 'max_res': 128, 'use_linear': False},
                {'hidden_dim': 16, 'log2_hashmap_size': 17, 'num_levels': 5, 'max_res': 256, 'use_linear': False}
            ],
            proposal_initial_sampler='piecewise',
            interlevel_loss_mult=1.0,
            distortion_loss_mult=0.002,
            orientation_loss_mult=0.0001,
            pred_normal_loss_mult=0.001,
            use_proposal_weight_anneal=True,
            use_appearance_embedding=True,
            use_average_appearance_embedding=True,
            proposal_weights_anneal_slope=10.0,
            proposal_weights_anneal_max_num_iters=1000,
            use_single_jitter=True,
            predict_normals=False,
            disable_scene_contraction=False,
            use_gradient_scaling=False,
            implementation='tcnn',
            appearance_embed_dim=32,
            average_init_density=0.01,
            camera_optimizer=CameraOptimizerConfig(
                _target=<class 'nerfstudio.cameras.camera_optimizers.CameraOptimizer'>,
                mode='SO3xR3',
                trans_l2_penalty=0.01,
                rot_l2_penalty=0.001,
                optimizer=None,
                scheduler=None
            )
        )
    ),
    optimizers={
        'proposal_networks': {
            'optimizer': AdamOptimizerConfig(
                _target=<class 'torch.optim.adam.Adam'>,
                lr=0.01,
                eps=1e-15,
                max_norm=None,
                weight_decay=0
            ),
            'scheduler': ExponentialDecaySchedulerConfig(
                _target=<class 'nerfstudio.engine.schedulers.ExponentialDecayScheduler'>,
                lr_pre_warmup=1e-08,
                lr_final=0.0001,
                warmup_steps=0,
                max_steps=200000,
                ramp='cosine'
            )
        },
        'fields': {
            'optimizer': AdamOptimizerConfig(
                _target=<class 'torch.optim.adam.Adam'>,
                lr=0.01,
                eps=1e-15,
                max_norm=None,
                weight_decay=0
            ),
            'scheduler': ExponentialDecaySchedulerConfig(
                _target=<class 'nerfstudio.engine.schedulers.ExponentialDecayScheduler'>,
                lr_pre_warmup=1e-08,
                lr_final=0.0001,
                warmup_steps=0,
                max_steps=200000,
                ramp='cosine'
            )
        },
        'camera_opt': {
            'optimizer': AdamOptimizerConfig(
                _target=<class 'torch.optim.adam.Adam'>,
                lr=0.001,
                eps=1e-15,
                max_norm=None,
                weight_decay=0
            ),
            'scheduler': ExponentialDecaySchedulerConfig(
                _target=<class 'nerfstudio.engine.schedulers.ExponentialDecayScheduler'>,
                lr_pre_warmup=1e-08,
                lr_final=0.0001,
                warmup_steps=0,
                max_steps=5000,
                ramp='cosine'
            )
        }
    },
    vis='viewer',
    data=PosixPath('data/nerfstudio/poster'),
    prompt=None,
    relative_model_dir=PosixPath('nerfstudio_models'),
    load_scheduler=True,
    steps_per_save=2000,
    steps_per_eval_batch=500,
    steps_per_eval_image=500,
    steps_per_eval_all_images=25000,
    max_num_iterations=30000,
    mixed_precision=True,
    use_grad_scaler=False,
    save_only_latest_checkpoint=True,
    load_dir=None,
    load_step=None,
    load_config=None,
    load_checkpoint=None,
    log_gradients=False,
    gradient_accumulation_steps={}
)
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
           Saving config to: outputs/poster/nerfacto/2024-05-29_074921/config.yml               experiment_config.py:136
           Saving checkpoints to: outputs/poster/nerfacto/2024-05-29_074921/nerfstudio_models             trainer.py:137
           Auto image downscale factor of 2                                                 nerfstudio_dataparser.py:484
Started threads
Setting up evaluation dataset...
Caching all 22 images.
Loading data batch ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:01
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
╭─────────────── viser ────────────────╮
│             ╷                        │
│   HTTP      │ http://0.0.0.0:34757   │
│   Websocket │ ws://0.0.0.0:34757     │
│             ╵                        │
╰──────────────────────────────────────╯
[NOTE] Not running eval iterations since only viewer is enabled.
Use --vis {wandb, tensorboard, viewer+wandb, viewer+tensorboard} to run with eval.
No Nerfstudio checkpoint to load, so training from scratch.
Disabled comet/tensorboard/wandb event writers
[07:49:36] Printing max of 10 lines. Set flag --logging.local-writer.max-log-size=0 to disable line        writer.py:448
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
### - Export Point Cloud
```
(nerfstudio) cv@cv-NERF:~/work$ ns-export pointcloud --load-config outputs/poster/nerfacto/2024-05-29_064436/config.yml --output-dir exports/pcd/ --num-points 1000000 --remove-outliers True --normal-method open3d --save-world-frame False
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.8/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

[07:41:40] Auto image downscale factor of 2                                                 nerfstudio_dataparser.py:484
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.8/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

Started threads
Setting up evaluation dataset...
Caching all 22 images.
Loading data batch ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:01
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
Loading latest checkpoint from load_dir
✅ Done loading checkpoint from outputs/poster/nerfacto/2024-05-29_064436/nerfstudio_models/step-000029999.ckpt
☁ Computing Point Cloud ☁ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 00:12
✅ Cleaning Point Cloud
✅ Estimating Point Cloud Normals
✅ Generated PointCloud with 1001840 points.
✅ Saving Point Cloud
(nerfstudio) cv@cv-NERF:~/work$ 
```

### - Export Mesh
```
(nerfstudio) cv@cv-NERF:~/work$ ns-export poisson --load-config outputs/poster/nerfacto/2024-05-29_064436/config.yml --output-dir exports/mesh/ --target-num-faces 50000 --num-pixels-per-side 2048 --num-points 1000000 --remove-outliers True --normal-method open3d
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.8/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

[07:43:31] Auto image downscale factor of 2                                                 nerfstudio_dataparser.py:484
Warning:
Unable to load the following plugins:

	libio_e57.so: libio_e57.so does not seem to be a Qt Plugin.

Cannot load library /home/cv/anaconda3/envs/nerfstudio/lib/python3.8/site-packages/pymeshlab/lib/plugins/libio_e57.so: (/lib/x86_64-linux-gnu/libp11-kit.so.0: undefined symbol: ffi_type_pointer, version LIBFFI_BASE_7.0)

Started threads
Setting up evaluation dataset...
Caching all 22 images.
Loading data batch ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:01
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
tiny-cuda-nn warning: FullyFusedMLP is not supported for the selected architecture 61. Falling back to CutlassMLP. For maximum performance, raise the target GPU architecture to 75+.
Loading latest checkpoint from load_dir
✅ Done loading checkpoint from outputs/poster/nerfacto/2024-05-29_064436/nerfstudio_models/step-000029999.ckpt
☁ Computing Point Cloud ☁ ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 00:12
✅ Cleaning Point Cloud
✅ Estimating Point Cloud Normals
✅ Generated PointCloud with 1001813 points.
✅ Computing Mesh this may take a while.
✅ Saving Mesh
Running meshing decimation with quadric edge collapse
Texturing mesh with NeRF
Unwrapping mesh with xatlas method... this may take a while.
✅ Unwrapped mesh with xatlas method━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 02:20
Creating texture image by rendering with NeRF...
Writing relevant OBJ information to files...
Writing vertices to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing vertices to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing vertex normals to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% ? 00:00
Writing faces to file ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 383916.56 lines-per-sec 00:00
────────────────────────────────────────────── 🎉 🎉 🎉 All DONE 🎉 🎉 🎉 ──────────────────────────────────────────────
                                          Unwrapped mesh using xatlas method.                                           
                                        Mesh has 25329 vertices and 50000 faces.                                        
                          Length of rendered rays to compute texture values: 5.518546104431152                          
                                        OBJ file saved to exports/mesh/mesh.obj                                         
                                     MTL file saved to exports/mesh/material_0.mtl                                      
                   Texture image saved to exports/mesh/material_0.png with resolution 2048x2048 (WxH)                   
────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
(nerfstudio) cv@cv-NERF:~/work$ 
```
