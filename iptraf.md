# iptraf

网络流量工具

```bash
pacman -S iptraf-ng
```

```bash
usage: iptraf-ng [options]
   or: iptraf-ng [options] -B [-i <iface> | -d <iface> | -s <iface> | -z <iface> | -l <iface> | -g]

    -h, --help            show this help message

    -i <iface>            start the IP traffic monitor (use '-i all' for all interfaces), 可以查看哪些远程主机在和本机通讯
    -d <iface>            start the detailed statistics facility on an interface, 显示指定网卡上的流量统计, 包括：各种速度和流量数据
    -s <iface>            start the TCP and UDP monitor on an interface, 显示 TCP/UDP 各个端口的流量数据
    -z <iface>            shows the packet size counts on an interface, 
    -l <iface>            start the LAN station monitor (use '-l all' for all LAN interfaces)
    -g                    start the general interface statistics, 显示每一个网卡上的流量数据

    -B                    run in background (use only with one of the above parameters
    -f                    clear all locks and counters
    -t <n>                run only for the specified <n> number of minutes
    -L <logfile>          specifies an alternate log file
```
