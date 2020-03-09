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

以管理员身份运行 PowerShell，然后执行下面的命令

```bash
Get-Service LxssManager | Restart-Service
```

或者手动去重启 LxssManager 服务。
