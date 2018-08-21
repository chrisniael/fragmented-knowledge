# 内网 socks5 代理

目标：在家里可以访问办公网网络。

## 安装 socks5 服务器

```bash
wget https://nchc.dl.sourceforge.net/project/ss5/ss5/3.8.9-8/ss5-3.8.9-8.tar.gz
tar xvf ss5-3.8.9-8.tar.gz
cd ss5-3.8.9
./configure
make
make install
```

## 配置启动 socks5 服务器


## 映射 socks5 服务端口至外网

* 公网服务器端配置

    下载 [dog tunnel](https://github.com/vzex/dog-tunnel)

    ```bash
    wget https://github.com/vzex/dog-tunnel/releases/download/lite_v1.34/dtunnel_linux_x64_1.34_lite.tgz;
    tar xvf dtunnel_linux_x64_1.34_lite.tgz
    mv dtunnel_lite /usr/local/bin/dtunnel_lite
    ```

    设置防火墙允许通过 8888/udp，61080/tcp (sock5 要映射到公网的端口)

    ```bash
    firewall-cmd --zone=public --add-port=8888/udp --permanent
    firewall-cmd --zone=public --add-port=61080/tcp --permanent
    firewall-cmd --reload
    ```

    增加 dog tunnel systemctl 配置, `vim /etc/systemd/system/dtunnel.service`

    ```cfg
    [Unit]
    Description=dog tunnel daemon
    After=syslog.target
    After=network.target

    [Service]
    Type=simple
    User=root
    Group=root
    ExecStart=/usr/local/bin/dtunnel_lite -service yourdomain.com:8888 -v -xor 123456 -auth 123456 -dnscache 10
    Restart=always
    RestartSec=10

    [Install]
    WantedBy=multi-user.target
    ```

    * `-sercice` : 服务器端监听的地址和端口，udp 协议，可以写公网 ip 或者域名
    * `-v` :
    * `-xor` :
    * `-auth` :
    * `-dnscache` :

    运行 dog tunnel server

    ```bash
    systemctl start dtunnel.service
    systemctl enable dtunnel.service
    ```

* 内网客户端配置

    下载 [dog tunnel](https://github.com/vzex/dog-tunnel), 同上。

    ```cfg
    [Unit]
    Description=dog tunnel daemon
    After=syslog.target
    After=network.target

    [Service]
    Type=simple
    User=root
    Group=root
    ExecStart=/usr/local/bin/dtunnel_lite -service shenyu.me:8888 -local :3000 -v -xor 18921661936 -auth 18921661936 -action 0.0.0.0:443 -pipe 5 -r
    Restart=always
    RestartSec=10

    [Install]
    WantedBy=multi-user.target
    ```

    运行 dog tunnel client

    ```bash
    systemctl start dtunnel.service
    systemctl enable dtunnel.service
    ```

    * `-sercice` : 服务器端监听的地址和端口，udp 协议，可以写公网 ip 或者域名
    * `-local` : 服务器端映射出去的端口
    * `-xor` :
    * `-action` :
    * `-pipe` :
    * `-r` :

## SwitchyOmega 配置


## ssh 配置
