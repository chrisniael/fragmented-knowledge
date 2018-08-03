# DogTunnel

[https://github.com/vzex/dog-tunnel](https://github.com/vzex/dog-tunnel)

## 远端

`vim /etc/systemd/system/dtunnel.service`

```cfg
[Unit]
Description=dog tunnel daemon
After=syslog.target
After=network.target

[Service]
Type=simple
User=root
Group=root
ExecStart=/usr/local/bin/dtunnel_lite -service shenyu.me:8888 -v -xor 123456 -auth 123456 
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
firewall-cmd --zone=public --add-port=8022/tcp --permanent
firewall-cmd --zone=public --add-port=8888/tcp --permanent
firewall-cmd --reload
firewall-cmd --list-al
```

## 近端

`vim /etc/systemd/system/dtunnel.service`

```cfg
[Unit]
Description=dog tunnel daemon
After=syslog.target
After=network.target

[Service]
Type=simple
User=root
Group=root
ExecStart=/usr/local/bin/dtunnel_lite -service shenyu.me:8888 -local :8022 -v -xor 123456 -auth 123456 -action 10.246.60.194:8022 -pipe 5 -r
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```bash
firewall-cmd --zone=public --add-port=8022/tcp --permanent
firewall-cmd --reload
firewall-cmd --list-al
```
