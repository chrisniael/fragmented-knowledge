# Gogs 使用 HTTPS


1. 使用 Let's Encrypt 生成证书，并设置自动更新证书
2. 配置 Nginx

    ```config
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
            proxy_pass http://localhost:3000;
        }
    }
    ```
3. 配置 Gogs

    ```config
    PROTOCOL         = http
    DOMAIN           = shenyu.me
    HTTP_PORT        = 3000
    ROOT_URL         = https://git.shenyu.me
    ```

    仅仅设置 `ROOT_URL` 为 `https://git.shenyu.me`，其他保持不变。

## 参考资料

[Setup Gogs with HTTPS (unknwon.io)](https://unknwon.io/setup-gogs-with-https)
