# Install Trojan

## Trojan

<https://github.com/Jrohy/trojan>

Ubuntu Minimal

```bash
apt update
apt upgrade
apt install vim
apt install net-tools
apt install cron  # 必须安装，否则 trojan-install 脚本在安装 https 证书时会出错，导致证书申请会失败
source <(curl -sL https://git.io/trojan-install)
```

安装完后输入'trojan'可进入管理程序  
浏览器访问 https://域名 可在线web页面管理 trojan 用户
