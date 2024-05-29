## Install

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
