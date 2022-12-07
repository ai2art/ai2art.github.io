---
title:  腾讯云最佳实践笔记
---

### 1. 优化ssh连接
  （1）修改 /etc/ssh/sshd_config

    ClientAliveInterval 30 
    ClientAliveCountMax 60

    systemctl restart ssh
  
  （2）启用root （optional）
    sudo passwd root 

  （3）添加 ssh key （略）

### 2. 挂载云盘
    （1）腾讯云盘的申请（略）
    （2）安装coscmd
        pip install coscmd
        pip install coscmd -U
        coscmd config -a <id> -s <key> -b <cos-name> -r ap-guangzhou -m 5 -p 1 --retry 5 --timout 60

        主要命令
        coscmd list
        coscmd upload -r <local/folder> <cos/folder>
        coscmd download -r  <cos/folder> <local/folder>

        参考 https://cloud.tencent.com/document/product/436/10976
    
    （3）挂载云盘到/cos

        https://github.com/tencentyun/cosfs/releases
        下载cosfs安装包并安装（dpkg -i xxxx.deb）

        echo <cos-name>:<id>:<key> > /etc/passwd-cosfs

        chmod 640 /etc/passwd-cosfs

        mkdir /cos
        cosfs <cos-name> /cos -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -oallow_other

### 3. 安装 miniconda

  （1）wget \
    https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && mkdir /root/.conda \
    && bash Miniconda3-latest-Linux-x86_64.sh -b \
    && rm -f Miniconda3-latest-Linux-x86_64.sh 

  （2）编辑 ~/.bashrc
    export PATH="/root/miniconda3/bin:${PATH}"

   (3) 修改conda 默认源（optional，可在environment.yaml中配置）
    conda config --show channels （查看现有源）
    conda config --remove-key channels（删除现有源）
    添加源：（略）

  （4）安装运行环境
    conda env update --name base --file environment.yaml --prune

### 4. 空间管理与清理
    df -h
    du -shx <folder>
    truncate -s 0 logfile

    常见可清理的大文件夹
    ./cache
    /var/log/
    /var/log/journal

