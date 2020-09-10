# CentOS sshd 配置 X11 转发

## 安装 xauth

```bash
yum install xorg-x11-xauth
```

## 配置 sshd

```config
X11Forwarding yes
XAuthLocation /bin/xauth
```
