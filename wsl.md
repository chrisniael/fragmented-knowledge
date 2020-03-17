# WSL


## 保持 Home 目录与 Windows 一致

```bash
sudo su -
vim /etc/passwd
```

WSL 默认 Home 目录在 `C:\Users\shenyu.tommy\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\shenyu`，在 WSL 中是没有权限访问这个目录的，所以在一些终端里，想要从 Windows 从 Home 目录启动是没有办法成功的，最后会被重定位到 `/` 目录。

把 `/home/shenyu` 改为 `/mnt/c/Users/shenyu`

https://jeremyskinner.co.uk/2018/07/27/sharing-home-directory-between-windows-and-wsl/

## 从 WSL 中打开资源管理器

```bash
explorer.exe .
explorer.exe 'C:\Users\shenyu\Desktop'
```
`explorer.exe ~/Desktop`  不能这样使用，只支持 Windows 全路径，所以要带上路径。要获取 WSL 下目录对应的 Windows 目录值，可以使用 `wslpath`。

```bash
wslpath -w "$PWD"
```

https://superuser.com/a/1343659


## 换行符兼容性处理

保持 Windows 上文件也用 `LF`，不要使用 Windows 自带的记事本，其他编辑器也改成使用 `LF` 换行符。

禁用 git 对 `CRLF` 的转化

```bash
git config --global core.autocrlf false
```

vim 使用 `LF` 换行符

```vim
set fileformat=unix
set fileformats=unix
```

https://blog.wzdxy.com/2018/11/wsl-start/

## 重启 WSL

1. 以管理员身份运行 PowerShell，然后执行下面的命令

   ```cmd
   Get-Service LxssManager | Restart-Service
   ```

2. 以管理员身份运行 CMD, 然后执行下面的命令

  ```cmd
  sc stop LxssManager
  sc start LxssManager
  ```

3. 手动去重启 LxssManager 服务。

## WSL 忘记用户密码

打开 CMD

```cmd
ubuntu config --default-user root
ubuntu
```

现在使用 root 登陆了 WSL

```bash
whoami
passwd shenyu
```

然后再把 WSL 的默认用户更改回去

```cmd
ubuntu config --default-user shenyu
```

* Ubuntu: ubuntu config --default-user root
* openSUSE Leap 42: openSUSE-42 config --default-user root
* SUSE Linux: SLES-12 config --default-user root
* Debian: debian config --default-user root
* Kali Linux: kali config --default-user root

## 关闭 Bell 声音

```bash
# /etc/inputrc
set bell-style none
```

## 升级 Ubuntu 至 19.10a

```bash
sudo su -
apt update
apt upgrade
cat /etc/os-release
```

打开 `/etc/update-manager/release-upgrades`，将 `Prompt` 的值改成 `normal`

```cfg
# /etc/update-manager/release-upgrades
Prompt=normal
```

```bash
apt update
do-release-upgrade -c
do-release-upgrade
cat /etc/os-release
```

期间会出现 Configuring lxd 询问，选 Skip。

## wsltty

1. 安装

   https://github.com/mintty/wsltty/releases

2. 配置快捷方式

   组件目录 : `%LOCALAPPDATA%/wsltty`

   双击运行这个目录中的下面这两个文件：

   * configure WSL shortcuts : 添加 WSL Terminal 至开始菜单
   * add default to context menu : 添加 WSL Terminal 至鼠标右键菜单

   然后就可以通过开始菜单和鼠标右键打开 WSL Terminal 了。

3. 配置 mintty

   配置目录 : `%APPDATA%/wsltty`

   https://github.com/chrisniael/gruvbox-contrib/tree/mintty-dark-white/mintty

   将 mintty 的 gruvbox 主题文件放在 `%APPDATA%/wsltty/themes` 目录下。

   * Looks - Theme - gruvbox-dark-medium
   * Looks - Cursor - Block
   * Looks - Cursor - No Blinking
   * Text - Font - 等距更纱黑体 T SC - 12
   * Text - Show bold - as font
   * Window - Scollbar - None
   * Terminal - Type - xterm-256color
   * Terminal - Bell - no beep

## 目录的默认访问权限

Windows 磁盘默认挂在在 `/mnt` 目录下，且目录的默认权限是 777。

在 WSL 中增加 `/etc/wsl.conf` 配置

```
# /etc/wsl.conf
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"
```

然后重启一下 WSL，使配置生效。


在 WSL 里新建目录的的权限也是 777，root 用户却是正常的 755。

在用户的 shell(.bashrc/.zshrc) 配置里增加下面这行配置

```bash
if [[ "$(umask)" = "000" ]]; then
  umask 022
fi
```

然后 source 一下 shell 的配置，或者重新登陆一下 WSL，使配置生效。

https://www.turek.dev/post/fix-wsl-file-permissions/

## 服务管理

WSL 中不能使用 systemctl 管理服务，只能通过 service 来管理，例如：

```bash
/etc/init.d/redis-server start
service redis-server start
```

且不能让服务开机自动启动。

https://github.com/MicrosoftDocs/WSL/issues/457
