# distcc

分布式编译系统，支持 C/C++, Objetive C/C++。

## 注意点

* 确保所有机器的操作系统和编译器一致，否则在编译 C++ 代码时可能会出现编译错误。
* distcc/distccd 版本确保一致，可能存在兼容性问题。
* 注意网络带宽瓶颈的评估，至少是千兆网。

## 服务器

```bash
distccd --no-detach --daemon --port --jobs 3632 --allow 10.246.34.0/24 --log-level error --log-file /tmp/distccd.log
```

* --no-detach: 不要 detach 启动 distccd 的 shell。
* --daemon: 单独运行 distccd 必须要指定这个参数。
* --port PORT: 指定 TCP 监听端口，如果不指定，默认使用 3632。
* --jobs JOBS: 同时可以接受的最大任务数量，如果不指定，默认值是 cpu 数量 + 2。
* --allow IPADDR[/MASK]: 允许连接 distccd 的客户端 ip。
* --log-level LEVEL: 日志等级， 可选值: critical, error, warning, notice, info, debug。
* --log-file FILE: 使用文件存放日志而不是 syslog。

可以通过 systemctl 来开机自动启动 distccd，不通发行版本的 distccd 的默认配置和配置文件路径可能有所不通，但是参照上面列举都能完成设置。


## 客户端

配置服务器列表

`~/.distcc/hosts`

```cfg
localhost/16
10.246.34.35/16,lzo
```

* /16 : 该 distccd 服务器接受的最大任务数量，如果不指定，默认值为 4。
* ,lzo : 在网络传输时使用 LZO 压缩。

更多 hosts 配置，`man distcc` HOST SPECIFICATIONS 章节。

查看当前 distcc hosts 配置

```bash
distcc --show-hosts
```

查看 distcc 能使用的最大并发任务数量

```bash
distcc -j
```

CMake 使用 distcc 编译

```bash
cmake -DCMAKE_C_COMPILER=/usr/lib/distcc/cc -DCMAKE_CXX_COMPILER=/usr/lib/distcc/c++ ..
make -j32
```

`/usr/lib/distcc/cc` 和 `/usr/lib/distcc/c++` 其实时 `/usr/bin/distcc` 的软连接。

`make -j` 数量别超过 `distcc -j` 的返回值。

或者直接设置环境变量 `CC` 和 `CXX`

```bash
export CC='distcc gcc'
export CXX='distcc g++'
```

查看当前编译任务

```bash
distccmon-text 3
```

每 3 秒刷新一下数据。

## 性能

discc 对于少量机器几乎可以线性扩展，单台 1700MHz Pentium IV machine 通过 distcc 编译 Linux 2.4.19 耗时 6 分 45 秒，3 台同样的机器通过 distcc 编译耗时 2 分 30 秒，快了 2.6 倍样子，理论上 3 台机器应该是快 3 倍，这里 distcc 的扩展效率达到了 89%。
