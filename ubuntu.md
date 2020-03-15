# Ubuntu

## 查看 ubuntu 发行版本

```
cat /etc/os-release
cat /etc/issue
lsb_release  # WSL 不会输出版本
```

## 修改 visudo 默认编辑器

```bash
su -
update-alternatives --config editor
```

然后输入 `3` 选择 `/usr/bin/vim.basic`。

这样其实是修改了系统的默认编辑器，其他命令也会用到这个配置。

## visudo 设置免密无效

```cfg
# Allow members of group sudo to execute any command
root    ALL=(ALL:ALL) ALL
shenyu  ALL=(ALL:ALL) NOPASSWD: ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

主要是 `shenyu` 属于 sudo 这个组，所以虽然上面设置了 `NOPASSWD`，但是被最后一行覆盖了。只要将 `shenyu  ALL=(ALL:ALL) NOPASSWD: ALL` 移到最后一行就可以了。

https://askubuntu.com/a/504666
