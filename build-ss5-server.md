# SS5 Server 搭建

```bash
yum -y install pam-devel
yum -y install openldap-devel
```

/etc/opt/ss5/ss5.conf

```cfg
auth    0.0.0.0/0               -              u
permit u        0.0.0.0/0       -       0.0.0.0/0       -       -       -       -       -
```

/etc/opt/ss5/ss5.passwd

```cfg
shenyu ******
```

/etc/sysconfig/ss5

```cfg
SS5_OPTS=" -u root -b 0.0.0.0:1080"
```

```bash
chmod 755 /etc/rc.d/init.d/ss5
```

```bash
systemctl daemon-reload
systemctl start ss5
systemctl enable ss5
```
