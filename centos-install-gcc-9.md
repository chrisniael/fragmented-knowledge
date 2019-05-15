# CentOS Install GCC 9.1 from Source

## Install Prerequists

```bash
yum install -y  binutils gzip bzip2 tar make gmp-devel mpfr-devel mpc-devel
```

## Compile and Install isl

```bash
wget ftp://gcc.gnu.org/pub/gcc/infrastructure/isl-0.18.tar.bz2
./configure --prefix=/usr
make
make install
ldconfig
```


## Compile and Install GCC

```bash
git clone https://github.com/gcc-mirror/gcc.git
git fetch
git tag
git checkout gcc-9_1_0-release
mkdir gcc-build
cd gcc-build
../gcc/configure --prefix=/usr/local/gcc-9.1 --enable-languages=c,c++ --disable-multilib
make
make install-strip
```
