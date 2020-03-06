# LLD

支持多线程链接，默认是开启的。

LLD 安装完后的可执行文件名字是 ld.lld。

## 使用

```bash
ln -s /path/to/ld.lld /usr/bin/ld so that /usr/bin/ld
```

或者

```bash
export LDFLAGS='-fuse-ld=lld'
```

LDD 会在编译后的可执行文件的 .comment 部分留下名字和版本号。可以执行如下命令检验是否成功使用 LDD：

```bash
readelf --string-dump .comment <output-file>
```

如果输出的字符串里有 `Linker: LLD` 则成功了。
