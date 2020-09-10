# macOS sshd 配置 X11 转发

## 安装 xQuartz

```bash
brew cask instal xquartz
```

## 配置 sshd

/etc/ssh/sshd_config

```config
X11Forwarding yes
XAuthLocation /opt/X11/bin/xauth
```
