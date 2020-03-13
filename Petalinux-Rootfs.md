# Petalinux-Rootfs
## rootfs镜像准备
从http://www.pynq.io/board.html 下载 PYNQ rootfs arm http://bit.ly/33fftBw 得到pynq_rootfs_arm_v2.5.zip
## 制作sd卡
使用Win32 Disk Imager http://forspeed.onlinedown.net/down/Win32DiskImager-0.9.5-binary.zip 将pynq_rootfs_arm_v2.5.zip解压出来的bionic.arm.2.5.img写入SD卡
## 更改启动分区镜像
将images/linux/BOOT.bin和images/linux/image.ub复制入SD卡第一分区
## 更改rootfs中ubuntu配置
### 1.更改网络配置
在`/etc/network/interfaces`中添加
    auto lo
    iface lo inet loopback

    allow-hotplug eth0
    iface eth0 inet dhcp
