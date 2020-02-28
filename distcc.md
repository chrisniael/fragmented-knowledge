# distcc

ccache（"compiler cache" 的缩写）会缓存编译生成的信息，并在编译的特定部分使用缓存的信息， 比如头文件依赖关系，这样就节省了通常使用 cpp 解析这些信息所需要的时间。

## 安装

```bash
yum install ccache  # CentOS
apt-get install ccache  # Ubuntu
pacman -S ccache  # Arch
```

## CMake 集成 ccache

在项目的 CMakeList.txt 中添加下面配置：

```cmake
find_program(CCACHE_FOUND ccache)
if(CCACHE_FOUND)
  set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE ccache)
  set_property(GLOBAL PROPERTY RULE_LAUNCH_LINK ccache)
endif(CCACHE_FOUND)
```

## ccache 配置

查看统计 ccache 统计信息

```bash
ccache -s
```

个人的配置路径：~/.ccache/ccache.conf

```cfg
max_size = 5.0G
```

更多配置请查看 https://ccache.dev/manual/latest.html

## 注意点

* ccache 并不会增加首次编译的速度，而是编译过一次后，ccache 会缓存一些编译要用的数据，来加快后续的编译速度。
* 编译过一次后，哪怕删除所有 CMake 的缓存文件重新编译，ccache 都能加快编译速度，因为 ccache 缓存文件依然有效。

