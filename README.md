# Petalinux2018.3 安装
## 1.ubuntu系统配置
安装ubuntu16.04.4  
更换国内源 apt update 一条龙一下  
用户名为fish
## 2.环境配置
### 1NFS服务 *以后编写linux驱动要用*
安装NFS服务

    sudo apt-get install nfs-kernel-server
在用户根目录下创建文件夹

    mkdir -p /home/fish/linux/nfs
在nfs配置文件`/etc/exports`中添加目录

    /home/fish/linux/nfs *(rw,sync,no_root_squash)
使改动生效

    sudo exportfs -rv
重启NFS服务

    sudo service nfs-kernel-server restart

查看共享目录

    showmount -e
### 2安装依赖库

    sudo apt-get install tofrodos iproute2 gawk gcc g++ git make net-tools libncurses5-dev tftpd zlib1g:i386 libssl-dev flex bison libselinux1 gnupg wget diffstat chrpath socat xterm autoconf libtool tar unzip texinfo zlib1g-dev gcc-multilib build-essential libsdl1.2-dev libglib2.0-dev screen pax gzip automake
### 3修改bash
    sudo dpkg-reconfigure dash
## 3.安装Petalinux
把opt的组换换

    sudo chown fish:fish /opt
整个安装文件夹

    mkdir -p /opt/pkg/petalinux/2018.3
安装到那个文件夹里去

    ./petalinux-v2018.3-final-installer.run /opt/pkg/petalinux/2018.3
## 4.安装SDK
    ./Xilinx_SDK_2018.3_1207_2324_Lin64.bin
## 5.使用Petalinux
https://github.com/FishYu-CN/Petalinux-18.3-tutorial/blob/master/Petalinux-build.md
