# CentOS 7 升级内核版本

## 检查内核版本

```bash
uname -sr
```

## 升级内核

```bash
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
yum --enablerepo=elrepo-kernel install kernel-ml
shutdown -h now
```

## 设置 GRUB

`vim /etc/default/grub`

```cfg
GRUB_DEFAULT=0
```

```bash
grub2-mkconfig -o /boot/grub2/grub.cfg
```

## 删除旧 kernel

```bash
yum remove kernel-3.* kernel-devel-3.*
```

## 参考

* [http://elrepo.org/tiki/tiki-index.php](http://elrepo.org/tiki/tiki-index.php)
* [https://elrepo.org/tiki/kernel-ml](https://elrepo.org/tiki/kernel-ml)
* [https://www.tecmint.com/install-upgrade-kernel-version-in-centos-7/](https://www.tecmint.com/install-upgrade-kernel-version-in-centos-7/)
