# Fragmented Knowledge

一些零碎的知识点记录。


## Windows 编译 Boost

打开 **x64 Native Tools Command Prompt for VS 2017**（不要使用 Windows 自带的 Cmd）

```
cd C:/boost_1_65_1/tools/build
bootstrap.bat
cp C:/boost_1_65_1/tools/build/bjam.exe C:/boost_1_65_1/
cd C:/boost_1_65_1
bjam add_ress-model=64
```

## Windows CMake 编译

```
cmake -G "Visual Studio 15 Win64"
cmake --build . --config Release
```

不指定 Win64 的话，生成的 Visual Studio 工程是 Win32 的，也以不指定 `--config Release`，默认编译的是 Debug 版。

## Windows 虚拟桌面快捷键

* Win + Tab ：显示所有虚拟桌面
* Ctrl + Win + D ：新键一个虚拟桌面
* Ctrl + Win + 左/右方向键 ：切换上/下一个虚拟桌面
* Win + Ctrl + F4 ：关闭当前的虚拟桌面

## CentOS 7 笔记本合盖不睡眠

修改配置 `/etc/systemd/logind.conf`

```
#HandleLidSwitch=suspend
HandleLidSwitch=lock
```

然后执行下面命令使配置生效

```
systemctl restart systemd-logind
```
