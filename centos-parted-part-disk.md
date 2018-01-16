# 使用 parted 分区

## 安装 parted

```bash
yum install -y parted
```

## 使用 parted 分区

```bash
parted /dev/sdb

mklabel gpt    # 指定分区类型
mkpart primary XFS 0% 100%    # 新建一个 XFS 格式的 primary 分区
p    # 查看所有的分区
quit    # 退出 Parted
```

## 格式化分区

```bash
mkfs.xfs -f /dev/sdb1
```


## 挂载分区

```bash
mount -t xfs /dev/sdb1 /data
```

验证是否挂载成功

```bash
df -Th /data
```

设置启动时自动挂载

编辑配置文件 `/etc/fstab`

```config
/dev/sdb1 /data xfs defaults 0 0
```
