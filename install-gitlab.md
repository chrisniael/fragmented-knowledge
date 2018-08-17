# 安装 GitLab

```bash
yum install -y curl policycoreutils-python openssh-server
systemctl enable sshd
systemctl start sshd
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
```

```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | bash
```

将 `EXTERNAL_URL` 的值设置为之后想要访问的 URL，可以是域名或者 IP 地址

```bash
EXTERNAL_URL="http://gitlab.example.com" yum install -y gitlab-ce
```

## 查看 GitLab 服务状态

```bash
systemctl status gitlab-runsvdir.service
```
