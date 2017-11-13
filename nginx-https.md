# Nginx 启用 HTTPS


## 安装 Let's Encrypt 客户端

```bash
yum install epel-release
```

```bash
yum install python2-certbot-nginx
```

## 配置 Nginx

```bash
yum install nginx
```

```bash
vi /etc/nginx/nginx.conf`
```

```config
server_name _;
```

```config
server_name example.com www.example.com;
```

```bash
nginx -t
```

```bash
systemctl reload nginx
```

## 配置防火墙

```bash
firewall-cmd --permanent --add-service=http
firewall-cmd --permanent --add-service=https
```

## 获取 SSL 证书

```bash
certbot --nginx -d example.com -d www.example.com
```


## 自动更新证书

```bash
crontab -e
```

```config
15 3 * * * /usr/bin/certbot renew --quiet
```


## 参考资料

[How To Secure Nginx with Let's encrypt on CentOS 7 (DigitalOcean Community)](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-centos-7)
