# 手动编译安装 zsh

## 编译安装

```bash
wget https://github.com/zsh-users/zsh/archive/zsh-5.8.zip
unzip zsh-5.8.zip
cd zsh-zsh-5.8/
./Util/preconfig
./configure
make
make install
```

## 修改默认 shell

```bash
vim /etc/shells
```

在最下面增加

```txt
...
/usr/local/bin/zsh
```

```bash
chsh -s /usr/local/bin/zsh <username>
```
