# Docker CentOS 安装 SSH 服务

```bash
docker pull centos
docker run -i -t centos /bin/bash

yum install openssh openssh-server openssh-clients vim passwd

ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key
ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key

vi /etc/pam.d/sshd    # 修改 pam_loginuid.so 为 optional

passwd

rm -rf /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

exit
```

```bash
docker ps -l
docker commit -m "Install sshd." 137c84959ff1 centos:sshd
```

```bash
docker run -d -p 8022:22 centos:sshd /usr/sbin/sshd -D
```
