# CentOS 7 ShadowSocks 客户端作 HTTP(S) 代理

```bash
wget https://copr.fedorainfracloud.org/coprs/librehat/shadowsocks/repo/epel-7/librehat-shadowsocks-epel-7.repo
mv librehat-shadowsocks-epel-7.repo /etc/yum.repos.d/
yum install -y shadowsocks-libev
```

/etc/shadowsocks-libev/config.json

```config
{
    "server" : "*.*.*.*",
    "server_port" : 8989,
    "local_port" : 1080,
    "password" : "****",
    "timeout" : 60,
    "method" : "chacha20-ietf-poly1305",
}
```

```bash
systemctl start shadowsocks-libev-local.service
systemctl enable shadowsocks-libev-local.service
```

```bash
curl --socks5 127.0.0.1:1080 http://httpbin.org/ip
```

```json
{
    "origin" : "*.*.*.*"
}
```

`origin` 字段的值是 ShadowSocks 服务器的 IP。


```bash
yum install -y privoxy
```

/etc/privoxy/config


确保这两行没有被注释掉

```config
listen-address 127.0.0.1:8118
forward-socks5t / 127.0.0.1:1080 .    #shadowsocks cli 的本地 IP 和端口
```

```bash
systemctl start privoxy.service
systemctl status privoxy.service
```


```bash
export http_proxy=http://127.0.0.1:8118       #privoxy 配置的 listen-address
export https_proxy=http://127.0.0.1:8118
```

```bash
curl www.google.com
```
