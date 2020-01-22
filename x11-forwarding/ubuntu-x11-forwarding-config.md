# Ubuntu X11 Forwarding

## 安装依赖

* sshd
* xauth

```bash
apt install openssh org-xauth
```

## sshd 配置

```config
# /etc/ssh/sshd_config

X11Forwarding yes
```

其他值用默认值就可以了。


## X11 connection rejected because of wrong authentication

配置环境变量 XAUTHORITY，可以放在 ~/.bashrc 中自动加载。

Arch 没有这样的问题，不需要配置环境变量 XAUTHORITY 就可以知道 .Xauthority 的位置。

```bash
export XAUTHORITY=$HOME/.Xauthority
```

* https://community.hpe.com/t5/Networking/X11-connection-rejected-because-of-wrong-authentication/td-p/6987197#.XiMluy3ogWl

## 客户端使用

#### 方法一

```bash
ssh -XY user@ubuntu-host
```

-X : Enables X11 forwarding.
-Y : Enables trusted X11 forwarding.

#### 方法二

```config
# ~/.ssh/config
Host ubuntu
    hostname 10.211.55.37
    port 22
    user shenyu
    ForwardX11 yes
    ForwardX11Trusted yes
```

```bash
ssh ubuntu
```
