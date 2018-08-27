# CentOS 安装 GitLab

CentOS 7.5.1804

```bash
yum install -y curl policycoreutils-python openssh-server
systemctl enable sshd
systemctl start sshd
firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https --permanent
firewall-cmd --reload
```

```bash
yum install postfix
systemctl start postfix
systemctl enable postfix
```

部分网络提供商会把 25 端口禁用，这样 postfix 功能会用不了。


```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | bash
```

将 `EXTERNAL_URL` 的值设置为之后想要访问的 URL，可以是域名或者 IP 地址

```bash
EXTERNAL_URL="http://gitlab.example.com" yum install -y gitlab-ce
```

## 配置 HTTPS

生成 SSL 证书

```bash
mkdir -p /etc/gitlab/ssl/private
mkdir -p /etc/gitlab/ssl/certs
chmod 700 /etc/gitlab/ssl/private
openssl req -x509 -nodes -days 36500 -newkey rsa:2048 -keyout /etc/gitlab/ssl/private/gitlab.key -out /etc/gitlab/ssl/certs/gitlab.crt
```

修改 GitLab 配置文件 `/etc/gitlab/gitlab.rb`

```cfg
nginx['redirect_http_to_https'] = true
nginx['ssl_certificate'] = "/etc/gitlab/ssl/certs/gitlab.crt"
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/private/gitlab.key"
```

生效配置

```bash
gitlab-ctl reconfigure
```

## Proxy

外部使用一台公网的服务器来转发所有 HTTPS 请求至内网服务器。

## Dog Tunnel 配置

...


## Nginx 配置

```cfg
upstream git.shenyu.me {
    server localhost:3000;
}

server
{
    listen      80;
    server_name git.shenyu.me;

    listen 443 ssl http2; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/shenyu.me/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/shenyu.me/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot

    if ($scheme != "https") {
        return 301 https://$host$request_uri;
    } # managed by Certbot

    location / {
        #proxy_set_header  X-Real-IP  $remote_addr;
        proxy_pass https://git.shenyu.me;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 参考

* [GitLab Installation (gitlab.com.cn)](https://www.gitlab.com.cn/installation/#centos-7)
* [Incorrect URL for builds and new projects when behind a proxy (gitlab.com)](https://gitlab.com/gitlab-org/gitlab-ce/issues/14888)
* [How To Set Up Nginx Load Balancing with SSL Termination (digitalocean.com)](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-load-balancing-with-ssl-termination)
* [Gitlab 安装，配置HTTPS证书、配置SMTP (cnyunwei.cc)](https://www.cnyunwei.cc/archives/1182)
* [如何在CentOS 7上为Nginx创建自签名的SSL证书 (howtoing.com)](https://www.howtoing.com/how-to-create-a-self-signed-ssl-certificate-for-nginx-on-centos-7/)
