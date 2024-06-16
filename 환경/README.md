# 환경 

ubuntu
    기본
        apt-get update --fix-missing
        apt-get upgrade
        apt-get install -y sudo vim git wget unzip curl htop locales build-essential software-properties-common
        passwd

    그룹
        groupadd conda
        chgrp -R conda ~/downloads/miniconda3
        chmod 770 -R ~/downloads/miniconda3

    유저
        useradd -m -g conda -s /bin/bash sjt
        ech~/downloads/miniconda3/etc/profile.d/conda.sh" >> /home/sjt/.bashrc
        echo "conda activate base" >> /home/sjt/.bashrc

    root
        usermod -G sudo -a sjt
        passwd sjt

    conda
        RUN mkdir -p ~/downloads/miniconda3 && \
            wget -q https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/downloads/miniconda3/miniconda.sh && \
            /bin/bash ~/downloads/miniconda3/miniconda.sh -b -u -p ~/downloads/miniconda3 && \
            rm -rf ~/downloads/miniconda3/miniconda.sh && \
            ln -s ~/downloads/miniconda3/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
            echo ". ~/downloads/miniconda3/etc/profile.d/conda.sh" >> ~/.bashrc && \
            echo "conda activate base" >> ~/.bashrc
        RUN conda update -n base -c defaults conda --force && \
            conda update -y --all
        RUN conda upgrade -n base conda
        RUN conda config --add channels defaults && \
            conda config --add channels r && \
            conda config --add channels bioconda && \
            conda config --add channels conda-forge
        
        pandas jupyter seaborn scikit-learn keras tensorflow jupyterlab

    jupyter
        conda install -c conda-forge jupyterlab
    
    pandas jupyter seaborn scikit-learn keras tensorflow jupyterlab

## 목적

### pytorch

### tensorflow