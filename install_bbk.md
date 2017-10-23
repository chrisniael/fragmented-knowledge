# CentOS 7 安装 Google BBR

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

