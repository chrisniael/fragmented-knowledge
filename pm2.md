# pm2

## 开机自动启动

```bash
pm2 save  ## dump all processes for resurrecting them later
pm2 startup
```

`pm2 save` 的作用是记录当前托管的 node 程序，如果不执行这个，重启机器后并不会重启托管的 node 服务。

## 关闭开机自动启动

```bash
pm2 unstartup
```

执行完后会会停止 pm2 的 daemon 进程。

## 停止 pm2 daemon 进程

```bash
pm2 kill
```
