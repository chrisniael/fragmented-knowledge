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

BOM（byte-order mark）：字节顺序标记

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

## Google Test 指定运行测试用例

```bash
./foo_test    没有指定过滤条件，运行所有案例
./foo_test --gtest_filter=*    使用通配符*，表示运行所有案例
./foo_test --gtest_filter=FooTest.*    运行所有“测试案例名称(testcase_name)”为FooTest的案例
./foo_test --gtest_filter=*Null*:*Constructor*    运行所有“测试案例名称(testcase_name)”或“测试名称(test_name)”包含Null或Constructor的案例。
./foo_test --gtest_filter=-*DeathTest.*    运行所有非死亡测试案例。
./foo_test --gtest_filter=FooTest.*-FooTest.Bar    运行所有“测试案例名称(testcase_name)”为FooTest的案例，但是除了FooTest.Bar这个案例
```

## CentOS 7 安装 Chrome

```bash
wget http://repo.fdzh.org/chrome/google-chrome-mirrors.repo -P /etc/yum.repos.d/
yum install google-chrome-stable
```

可以把 CentOS 7 自带的 firefox 卸载

```bash
yum remove firefox
```

## Terminator

CentOS 7 自带的终端并不是很好用，Terminator 会相对好用一点。

```bash
yum install terminator
```

## Terminator 快捷键

* `Ctrl` + `PageUp` : 上一个标签
* `Ctrl` + `PageUp` : 下一个标签
* `F11` : 全屏
* `Ctrl` + `Shift` + `O` : 水平分割终端
* `Ctrl` + `Shift` + `E` : 垂直分割终端
* `Ctrl` + `Shift` + `W` : 关闭当前终端
* `Ctrl` + `Shift` + `T` : 打开一个新的标签页
* `Alt` + `↑` : 切换至上面的终端
* `Alt` + `↓` : 切换至下面的终端
* `Alt` + `←` : 切换至左边的终端
* `Alt` + `↓` : 切换至右边的终端

## Vimium

Chrome 的插件，能让用户使用类似 Vim 的快捷键来操作 Chrome。

## iconv

iconv 是内建 glibc 的组成部分，所以没有独立出 shared-library。

## 网络顺序 & 主机顺序：

Little endian
Big endian

## Git 查看远程分支

```bash
git branch -a
```

## Git Clone 远程分支

```bash
git checkout -t origin/newbranch
```

或者

```bash
git checkout -b newbranch origin/newbranch
```

## 读写锁

## 递归锁

## memset

```cpp
void * memset(void * ptr, int value, size_t num);
```

## memcpy

```cpp
void * memcpy(void * destination, void * source, size_t num);
```

## C++ 宏 \#

在一个宏中的参数前面使用一个#，预处理器会把这个参数转换为一个字符数组。

```cpp
#define ERROR_LOG(module)   fprintf(stderr,"error: "#module"\n")
ERROR_LOG("add");        //转换为 fprintf(stderr,"error: "add"\n");
ERROR_LOG(devied =0);    //转换为 fprintf(stderr,"error: devied=0\n");
```

## C++ 宏 \#\#

“##” 是一种分隔连接方式，它的作用是先分隔，然后进行强制连接。

```cpp
#define TYPE1(type,name)   type name_##type##_type
#define TYPE2(type,name)   type name##_##type##_type
TYPE1(int, c);    //转换为: int name_int_type; (因为##号将后面分为 name_ 、type 、 _type三组，替换后强制连接)
TYPE2(int, d);    //转换为: int d_int_type; (因为##号将后面分为 name、_、type 、_type四组，替换后强制连接)
```

## C++ 宏 do{ }while(0)

采用这种方式是为了防范在使用宏过程中出现错误，主要有如下几点：

1. 空的宏定义避免warning

  ```cpp
  #define foo() do{}while(0)
  ```

2. 存在一个独立的block，可以用来进行变量定义，进行比较复杂的实现。
3. 如果出现在判断语句过后的宏，这样可以保证作为一个整体来是实现

  ```cpp
  #define foo(x) \
  action1(); \
  action2();
  ```

  在以下情况下

  ```cpp
  if(NULL == pPointer)
      foo();
  ```

  就会出现action1和action2不会同时被执行的情况，而这显然不是程序设计的目的。
4. 以上的第3种情况用单独的 `{}` 也可以实现，但是为什么一定要一个 `do{}while(0)` 呢，看以下代码

  ```cpp
  #define switch(x,y) {int tmp; tmp="x";x=y;y=tmp;}
  if(x>y)
      switch(x,y);
  else
      //error, parse error before else
      otheraction();
  ```

  在把宏引入代码中，会多出一个分号，从而会报错。这对这一点，可以将if和else语句用 `{}` 括起来，可以避免分号错误。

  使用 `do{…}while(0)` 把它包裹起来，成为一个独立的语法单元，从而不会与上下文发生混淆。同时因为绝大多数的编译器都能够识别 `do{…}while(0)` 这种无用的循环并进行优化，所以使用这种方法也不会导致程序的性能降低。

## 宽字符 wchar_t

## Terminal 字体推荐

Monaco 是一个来自 Mac 的字体，而 Consolas 是来自 Windows 的字体

## rpm 搜索拥有目标文件的软件包

```bash
rpm -qf target_file
```

## yum 搜索包含目标文件的软件包

```bash
yum whatprovides(provides) target_file
```

## gdb 调试 core 文件

```bash
ulimit -c unlimited
g++ -g
gdb ./bin/test core
bt
```

## CentOS 查看电池电量

```bash
cat /sys/class/power_supply/BAT1/capacity
```

## rpm

```bash
rpm -ivh foo-1.0-l.i386.rpm
rpm -Uvh foo-2.0-l.i386.rpm
rpm -e foo
rpm -q foo
碰到一个人不出来的文件，想要知道它是属于那一个软件包
rpm -qf /etc/nginx/nginx.conf
想了解某个文件包将会在系统里安装那些文件
rpm -qpi koules-1.2-2.i386.rpm
不小心误删了几个文件，但不确定到底是那些文件，可以对整个系统进行校验，以了解哪些部分可能已经损坏
rpm -Va
一个 RPM 包的文件都安装到哪里去了 
rpm -ql
```

## Vim 代码折叠

* zC 对所在范围内所有嵌套的折叠点进行折叠
* zo 展开折叠
* zO 对所在范围内所有嵌套的折叠点展开
* [z 到当前打开的折叠的开始处。
* ]z 到当前打开的折叠的末尾处。
* zj 向下移动。到达下一个折叠的开始处。关闭的折叠也被计入。
* zk 向上移动到前一折叠的结束处。关闭的折叠也被计入。

## CentOS 7 虚拟桌面快捷键

* `Ctrl` + `Alt` + `↑` : 切换到上一个虚拟桌面
* `Ctrl` + `Alt` + `↓` : 切换到下一个虚拟桌面
* `Ctrl` + `Alt` + `Shift` + `↑` : 将当前程序移动到上一个虚拟桌面
* `Ctrl` + `Alt` + `Shift` + `↓` : 将当前程序移动到下一个虚拟桌面

## Git Submodule

```bash
git submodule init
git submodule update
```
