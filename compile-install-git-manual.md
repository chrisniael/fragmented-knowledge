# 编译安装 git

```bash
yum install -y asciidoc xmlto docbook2X
ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi
```

```bash
git clone https://github.com/git/git.git
cd git
git checkout v2.21.0
make configure
./configure
make all doc info
make install install-doc install-html install-info
```
