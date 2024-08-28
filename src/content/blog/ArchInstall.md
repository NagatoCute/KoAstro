---
title: '安装 Arch Linux 的踩坑日记'
description: '使用VMware安装，版本号archlinux-2024.08.01-x86_64'
pubDate: 'Aug 28 2024'
heroImage: 'data:image/jpeg;base64,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'
pinned: false
---
> 本文发布于2024-8-28，请注意时效。
> 
> 主体是[官网的教程](https://archlinuxstudio.github.io/ArchLinuxTutorial/#/rookie/basic_install)，但是融合了各种踩坑

# 基础的无图形化界面
## 前期准备：
- 在[官网](https://archlinux.org/download/)下载好iso文件
- VMware创建虚拟机，选择iso文件，选择其它Linux里面最新的那个
- 选择配置，网络我选的是桥接模式
- 之后别着急启动，打开 `编辑虚拟机设置->选项->高级->固件类型->UEFI`

之后就可以启动了。
## 安装过程：
### 0.禁用 reflector
reflector 会为你选择速度合适的镜像源，但其结果并不准确，同时会清空配置文件中的内容，对于新人来讲并不适用，我们首先对其进行禁用。
```shell
systemctl stop reflector.service
```
 ### 1.再次确保是否为 UEFI 模式
在一系列的信息刷屏后，可以看到已经以 root 登陆安装系统了，此时可以执行的命令：
```shell
ls /sys/firmware/efi/efivars
```
若输出了一堆东西，即 efi 变量，则说明已在 UEFI 模式。否则请确认你的启动方式是否为 UEFI。

### 2.检测网络连接
因为是虚拟机，所以直接ping
```shell
ping www.baidu.com
```
### 3.更新系统时钟
```shell
timedatectl set-ntp true    #将系统时间与网络时间进行同步
timedatectl status          #检查服务状态
```
### 4.开始分区
#### 4.1.建立硬盘分区(这里使用cfdisk演示)
```shell
cfdisk
```
选择gpt

<img src="https://pica.zhimg.com/80/v2-902e7eb8544f74c1f9919365d1587508_720w.webp" alt="图像" class="responsive-image" />

之后可以参考[这个视频](https://www.bilibili.com/video/BV1J34y1f74E/)的前期部分的内容，进行分区

格式化和挂载分区也是参考上方视频。

在挂载时，挂载是有顺序的，先挂载根分区，再挂载 EFI 分区。 这里的 sdax 只是例子，具体根据你自身的实际分区情况来。

### 5.添加镜像源
使用如下命令编辑镜像列表：
````shell
vim /etc/pacman.d/mirrorlist
````

其中的首行是将会使用的镜像源。添加中科大或者清华的放在最上面即可。
```shell
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch

```
### 6.安装系统
#### 6.1.安装基础包
因为很重要所以着重提醒

VMware虚拟机不应该使用官网的
```shell
# VMware不要用这个
pacstrap /mnt base base-devel linux linux-headers linux-firmware 
```

而是使用
```shell
pacstrap /mnt base base-devel linux-lts btrfs-progs
```
- linux-lts：长期支持的内核软件包（LTS）。
#### 6.2.之后，安装其它必要的功能性软件：
```shell
pacstrap /mnt networkmanager vim sudo zsh zsh-completions
```
### 7.生成 fstab 文件
fstab 用来定义磁盘分区
````shell
genfstab -U /mnt >> /mnt/etc/fstab
````
复查一下 /mnt/etc/fstab 确保没有错误
```shell
cat /mnt/etc/fstab
```
### 8.change root
把环境切换到新系统的/mnt 下
```shell
arch-chroot /mnt
```
### 9.时区设置
设置时区，在`/etc/localtime` 下用/usr 中合适的时区创建符号连接。如下设置上海时区。
```shell
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```
随后进行硬件时间设置，将当前的正确 UTC 时间写入硬件时间。
```shell
hwclock --systohc
```
### 10.本地化
设置 Locale 进行本地化
Locale 决定了地域、货币、时区日期的格式、字符排列方式和其他本地化标准。

首先使用 vim 编辑 /etc/locale.gen，去掉 en_US.UTF-8 所在行以及 zh_CN.UTF-8 所在行的注释符号（#）。
```shell
vim /etc/locale.gen
```

然后使用如下命令生成 locale。
```shell
locale-gen
```

最后向 `/etc/locale.conf` 导入内容
```shell
echo 'LANG=en_US.UTF-8'  > /etc/locale.conf
```
注意，这里是英文本地化

不推荐在此设置任何中文 locale，会导致 tty 乱码。
### 11.设置主机名
首先在/etc/hostname设置主机名
```shell
vim /etc/hostname
```

加入你想为主机取的主机名，这里比如叫 myarch。

接下来在`/etc/hosts`设置与其匹配的条目。
```shell
vim /etc/hosts
```

加入如下内容
```shell
127.0.0.1   localhost
::1         localhost
127.0.1.1   myarch
```

### 12.为 root 用户设置密码
```shell
passwd root
```
打密码显示不出来是正常的
### 13.安装微码
```shell
pacman -S intel-ucode   #Intel
pacman -S amd-ucode     #AMD
#根据自己二选一
```
### 14.安装引导程序

安装必要的包：

```bash

pacman -S grub efibootmgr os-prober
```
安装 GRUB 到 EFI 分区：

```bash
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=ARCH
```
编辑 `/etc/default/grub` 文件：

```bash
vim /etc/default/grub
```
进行如下修改：

- 去掉 `GRUB_CMDLINE_LINUX_DEFAULT` 中的 `quiet` 参数。
- 将 `loglevel` 设置为 `5`。
- 添加 `nowatchdog` 参数。 （即，把 quiet 换成 nowatchdog）
- 添加 `GRUB_DISABLE_OS_PROBER=false`。
- 
生成 GRUB 配置文件：

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```
### 15.完成安装
退出 chroot 环境：

```bash
exit
```
卸载新分区：

```bash
umount -R /mnt
```
重启系统：

```bash
reboot
```
确保在重启前拔掉安装介质，以避免再次进入安装程序。

## 安装完成以后
### 网络配置：
哪怕是虚拟机这时候也需要配置网络了

启动并启用 NetworkManager：
```bash
systemctl enable --now NetworkManager
```
测试网络连接：
```bash
ping www.bilibili.com
```
### 安装neofetch
```shell
pacman -S neofetch
```
查看：
```shell
neofetch
```
### 系统关机：

```bash
shutdown -h now
```
或

```bash
poweroff
```



