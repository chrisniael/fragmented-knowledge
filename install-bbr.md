# 安装 Google BBR


## CentOS 7

```bash
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm
yum --enablerepo=elrepo-kernel install kernel-ml
```

查看当前已经安装的内核

```bash
awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
```

```bash
grub2-set-default 0
reboot
```

如果用的是 Google Cloud Platform 的话，系统会变为 Read-only，执行下 `mount -o remount rw /` 就可以了。

重启后，编辑 /etc/sysctl.conf，增加下面的配置

```
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
```

然后执行

```bash
sysctl -p
```

检测 BBR 是否正常启用，执行

```bash
sysctl net.ipv4.tcp_available_congestion_control
```

如果显示的值第一个是 bbr，则证明 BBR 已经正常启用。

```
net.ipv4.tcp_available_congestion_control = bbr cubic reno
```

## Amazon Linux AMI

内核版本已大于 4.7，不需要升级内核，只需要启用 BBR 即可

```bash
modprobe tcp_bbr
modprobe sch_fqj
sysctl -w net.ipv4.tcp_congestion_control=bbr
```

持久化配置

新建文件 `/etc/sysconfig/modules/tcpcong.modules`

内容如下

```bash
#!/bin/bash
exec /sbin/modprobe tcp_bbr >/dev/null 2>&1
exec /sbin/modprobe sch_fq >/dev/null 2>&1
```

```bash
chmod 755 /etc/sysconfig/modules/tcpcong.modules
echo "net.ipv4.tcp_congestion_control = bbr" >> /etc/sysctl.d/00-tcpcong.conf
```

## 参考

[amazon-linux-ami (aws.amazon.com)](https://aws.amazon.com/cn/amazon-linux-ami/2017.09-release-notes/)
