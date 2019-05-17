# Arch Linux 安装指南

## 下载 Arch Linux 镜像

https://www.archlinux.org/download/

## 验证镜像完整性

```bash
md5 archlinux-2019.05.02-x86_64.iso
```

## 镜像写入 U 盘

* Linux/Unix: dd
* MacOS: [balenaEtcher](https://github.com/balena-io/etcher)
* Windows: [USBWriter](https://sourceforge.net/projects/usbwriter/)

## 从 U 盘启动 Arch live 环境

 
## 验证启动模式

```
ls /sys/firmware/efi/efivars
```

* UEFI
* BIOS

## 连接 internet

#### 查看连接

```bash
ip link
```

#### 连接

对于有线网络，安装镜像启动的时候，默认会启动 dhcpcd，如果没有启动，可以手动启动

```bash
dhcpcd
```

#### 验证连接

```bash
ping shenyu.me
```

## 更新系统时间

```
timedatectl set-ntp true
timedatectl set-timezone Asia/Shanghai
```

## 磁盘分区



## 磁盘格式化

格式化 EFI System 分区

```bash
mkfs.fat -F32 /dev/nvme0n1p1
```

格式化 Linux root 分区

```bash
mkfs.ext4 /dev/nvme0n1p2
```

格式化 Linux swap 分区

```bash
mkswap /dev/nvme0n1p3
swapon /dev/nvme0n1p3
```

## 挂载文件系统

```bash
mount /dev/nvme0n1p2 /mnt
mkdir /mnt/boot
mount /dev/nvme0n1p1 /mnt/boot
```

## 配置 pacman mirror

```bash
vim /etc/pacman.d/mirrorlist
```

## 安装 Arch 和 Package Group

```bash
pacstrap /mnt base base-devel
```

## 生成 fstab 文件

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

## 切换至安装好的 Arch

```bash
arch-chroot /mnt
```

## 设置时区

```bash
timedatectl set-ntp true
timedatectl set-timezone Asia/Shanghai
hwclock --systohc
```

## 本地化

修改 /etc/locale.gen

```
# /etc/locale.gen

en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
```

创建 /etc/locale.conf

```
# /etc/locale.conf

LANG=en_US.UTF-8
```

## 网络配置

```
# /etc/hostname

beta
```

```
/etc/hosts

127.0.0.1    localhost
::1          localhost
```

```bash
systemctl enable dhcpcd
```

## 修改 root 密码

```bash
passwd
```

## 安装 Microcode

* AMD CPU
  
  ```bash
  pacman -S amd-ucode
  ```

* Intel CPU

    ```bash
    pacman -S intel-ucode
    ```

## 安装 GRUB

```bash
pacman -S grub
pacman -S efibootmgr
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=grub
grub-mkconfig -o /boot/grub/grub.cfg
```

## 安装图形界面

```bash
pacman -S gnome gnome-extra
systemctl enable gdm
```

## 重新启动

```bash
exit    # 退出 chroot 环境
reboot
```
