# Petalinux 首次编译
我这里使用zynq xc7z010
## 1.vivado导出硬件
File > Export >Export hardware  
记得勾选`Include bitstream`
把*.sdk那个文件夹弄过来备用
## 2.设置环境变量
    source /opt/pkg/petalinux/2018.3/settings.sh
该命令只对当前终端有效，重新打开终端后需要重新执行这一步。
## 3.创建工程
在用户根目录下创建`work/petalinux`文件夹并进入

    cd
    mkdir -p work/petalinux/
    cd work/petalinux/
创建名为`zynq_linux`的工程，模板使用`zynq`

    petalinux-create -t project --template zynq -n zynq_linux
## 4.配置工程
进入工程文件夹

    cd zynq_linux
导入硬件文件开始配置工程

    petalinux-config --get-hw-description /mnt/hgfs/share/zynq_petalinux.sdk/
配置完成后`save`然后`exit` *大多数默认配置即可启动*  

之后硬件文件不变配置工程可使用

    petalinux-config
## 5.配置内核
    petalinux-config -c kernel
配置完成后`save`然后`exit` *大多数默认配置即可启动*
## 6.配置根文件系统
    petalinux-config -c rootfs
配置完成后`save`然后`exit` *大多数默认配置即可启动*
## 7.配置设备树文件
    vi project-spec/meta-user/recipes-bsp/device-tree/files/system-user.dtsi
*这个文件可得好好改改，不然能启动但会卡在驱动加载*
## 8.编译工程
    petalinux-build
## 9.制作BOOT文件
    petalinux-package --boot --fsbl ./images/linux/zynq_fsbl.elf --fpga --u-boot --force
## 10.完成
将`images/linux/BOOT.bin`和`images/linux/image.ub`拷入SD卡，即可启动
