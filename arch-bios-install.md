# Arch Linux (BIOS/MBR) 安装指南

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

在 BIOS 中设置启动磁盘为刚刚写入 Arch 系统的 U 盘

进入 U 盘的启动引导程序后，选择第一项：Boot Arch Linux (x86_64)

## 验证启动模式

```
ls /sys/firmware/efi/efivars
```

如果 /sys/firmware/efi/efivars 目录存在，则系统可能是从 UEFI 模式启动的。

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

#### 查看磁盘设备

```bash
fdisk -l
```

#### 新建分区表

```bash
fdisk /dev/sda
```

下面的操作是在 fdisk 里

1. 输入 `o`，新建 DOS 分区表
2. 输入 `w`，保存修改，这个操作会抹掉磁盘所有数据，慎重

#### 分区创建

```bash
fdisk /dev/sda
```

1 sector = 512 bytes

1. 新建 Linux root 分区
   1. 输入 `n`
   2. 选择分区类型（p：主分区，e：扩展分区），默认选择 p ，直接 `Enter`
   3. 选择分区区号，直接 `Enter`，使用默认值，fdisk 会自动递增分区号
   4. 分区开始扇区号，直接 `Enter`，使用默认值
   5. 分区结束扇区号，例如：`+100G`（剩余空间 - 分配给 swap 分区的空间）
   6. 输入 `t` 修改刚刚创建的分区类型
   7. 选择分区号，直接 `Enter`， 使用默认值，fdisk 会自动选择刚刚新建的分区
   8. 输入 `83`，使用 Linux 类型
2. 新建 Linux swap 分区
   1. 输入 `n`
   2. 选择分区类型（p：主分区，e：扩展分区），默认选择 p ，直接 `Enter`
   3. 选择分区区号，直接 `Enter`，使用默认值，fdisk 会自动递增分区号
   4. 分区开始扇区号，直接 `Enter`，使用默认值
   5. 分区结束扇区号，例如 `+8G`
   6. 输入 `t` 修改刚刚创建的分区类型
   7. 选择分区号，直接 `Enter`， 使用默认值，fdisk 会自动选择刚刚新建的分区
   8. 输入 `82`，使用 Linux swap 类型
3. 保存新建的分区
   1. 输入 `w`

## 磁盘格式化

格式化 Linux root 分区

```bash
mkfs.ext4 /dev/sda1
```

格式化 Linux swap 分区

```bash
mkswap /dev/sda2
swapon /dev/sda2
```

如果格式化失败，可能是磁盘设备存在 Device Mapper

###### 显示 dm 状态

```bash
dmsetup status
```

###### 删除 dm

```bash
dmsetup remove <dev-id>
```

## 挂载文件系统

```bash
mount /dev/sda1 /mnt
```

## 配置 pacman mirror

```bash
pacman -S vim
```

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

生成 locale 信息

```bash
locale-gen
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
pacman -S dhcpcd
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
grub-install --target=i386-pc /dev/sda
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