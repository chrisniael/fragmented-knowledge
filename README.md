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

## VCPKG

Visual Studio 包管理器，不用手动引入库文件目录，自动加载，相当方便。

[https://github.com/Microsoft/vcpkg](https://github.com/Microsoft/vcpkg)

```
vcpkg install boost:x32-windows
vcpkg install boost:x64-windows
vcpkg --help
```

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

## Linux 上 包含 BOM 头的 UTF-8 文件

Vim 有处理 BOM 的功能，先将编码设置为 UTF-8，`:set fileencoding=utf-8`

* `:set bomb`
* `:set nobomb`
* `:set bomb?`

查找删除 BOM

```bash
grep -r -I -l $'^\xEF\xBB\xBF' /path
grep -r -I -l $'^\xEF\xBB\xBF' /path | xargs sed -i 's/^\xEF\xBB\xBF//;q'
```

## LSB

Linux标准规范（Linux Standard Base）/ 最低有效位（Least Significant Bit）

## MSB

最高有效位（Most Significant Bit）

## Windows 文件内容在 Linux 上乱码

```bash
iconv -f GB2312 -t UTF-8 source.cpp > destination.cpp
```
./foo_test    没有指定过滤条件，运行所有案例
./foo_test --gtest_filter=*    使用通配符*，表示运行所有案例
./foo_test --gtest_filter=FooTest.*    运行所有“测试案例名称(testcase_name)”为FooTest的案例
./foo_test --gtest_filter=*Null*:*Constructor*    运行所有“测试案例名称(testcase_name)”或“测试名称(test_name)”包含Null或Constructor的案例。
./foo_test --gtest_filter=-*DeathTest.*    运行所有非死亡测试案例。
./foo_test --gtest_filter=FooTest.*-FooTest.Bar    运行所有“测试案例名称(testcase_name)”为FooTest的案例，但是除了FooTest.Bar这个案例
```
