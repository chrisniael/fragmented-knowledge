# CentOS Install protobuf from Source

## Install Prerequists

```bash
yum install -y autoconf automake libtool make gcc-c++ unzip
```

## Compile and Install protobuf

```bash
./configure --prefix=/usr --disable-shared
make
make check
make install
```

## Reference

* [https://github.com/protocolbuffers/protobuf/blob/master/src/README.md](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md)
