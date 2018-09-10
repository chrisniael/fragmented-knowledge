# Mac VimIM

## 安装 berkeley-db 6.1.26

```bash
wget http://download.oracle.com/berkeley-db/db-6.1.26.tar.gz
tar xvf db-6.1.26.tar.gz
cd db-6.1.26/build_unix
mkdir -p /usr/local/Cellar/berkeley-db/6.1.26
../dist/configure --prefix=/usr/local/Cellar/berkeley-db/6.1.26
make
make install
db_archive -V
```

## 安装 berkeley-db for python

```bash
sudo su -
easy_install pip
YES_I_HAVE_THE_RIGHT_TO_USE_THIS_BERKELEY_DB_VERSION=1 BERKELEYDB_DIR=/usr/local/Cellar/berkeley-db/6.1.26 pip install bsddb3
```

## 配置 VimIM
