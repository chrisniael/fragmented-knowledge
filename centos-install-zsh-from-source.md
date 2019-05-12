# CentOS Install zsh From Source

## Install TeXinfo

```
yum install -y texinfo
```

## Build and Install Icmake

```
git clone https://gitlab.com/fbb-git/icmake.git
cd icmake/icmake
vim bootstrap/flags
```

```diff
diff --git a/icmake/bootstrap/flags b/icmake/bootstrap/flags
index 25a6127..52f18f7 100644
--- a/icmake/bootstrap/flags
+++ b/icmake/bootstrap/flags
@@ -8,7 +8,7 @@ fi
 . ../tmp/INSTALL.sh

 if [ "${CFLAGS}" == "" ] ; then
-    CFLAGS="-Wall -O2"
+    CFLAGS="-std=gnu99 -Wall -O2"
 fi

 if [ "${CC}" == "" ] ; then
```

这里不可以用 `-std=c99`，编译会报错

```bash
./icm_prepare /
./icm_bootstrap x
./icm_install all
```

## Build and Install YODL

gcc 需要支持 `-std=c++17` 选项，gcc 8.2.1 支持

```
yum install -y texlive texlive-*
git clone https://gitlab.com/fbb-git/yodl.git

cd yodl/yodl

./build programs
./build macros
./build man
./build manual

./build install programs /
./build install man /
./build install manual /
./build install macros
./build install docs
```

## Build and Install zsh

```bash
git clone https://github.com/zsh-users/zsh.git
git tag
git checkout zsh-5.7.1
./Util/preconfig
./configure
make
make check
make install
make install.info
```
