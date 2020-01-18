# Parallel Desktop Install Arch Linux With Gnome Desktop

## 安装 Arch 系统

...

## 安装 Gnome

安装通用的显卡驱动

```bash
pacman Ss gnome
# pacman Ss xorg gnome
systemctl enable gdm.service
pacman -S xf86-video-vesa
```

禁用 Wayland 替代 Xorg，这步是必须的，虚拟的显卡似乎不支持 Wayland，不禁用会启动不了 Gnome 桌面

```conf
# /etc/gdm/custom.conf

WaylandEnable=false
```

## 安装 Parallels Tool

```bash
pacman -Ss dkms
pacman -Ss linux-headers
create /mnt/cdrom
mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
./install
```

然后重启

## 配置 Gnome 网络设置界面


```bash
pacman -S networkmanager
systemctl enable NetworkManager.service
systemctl start NetworkManager.service
```

如果 Gnome 应用网络还没有通的话，点一下右上角菜单的网络开关，关掉再开应该就好了。

## 显示中文字体和 emoji 表情

```bash
pacman -S noto-font-cjk
pacman -S noto-font-emoji
```

## 输入法

Todo
