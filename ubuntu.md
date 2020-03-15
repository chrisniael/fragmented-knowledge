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
