# Fragmented Knowledge

这里是一些零碎知识点的记录，内容比较随意。


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

先

```
git fetch origin
```

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
# 检查
rpm -ivh --test foo-1.0-l.i386.rpm
rpm -Uvh foo-2.0-l.i386.rpm
rpm -e foo
rpm -q foo
# 碰到一个人不出来的文件，想要知道它是属于那一个软件包
rpm -qf /etc/nginx/nginx.conf
# 想了解某个文件包将会在系统里安装那些文件
rpm -qpi koules-1.2-2.i386.rpm
# 不小心误删了几个文件，但不确定到底是那些文件，可以对整个系统进行校验，以了解哪些部分可能已经损坏
rpm -Va
# 一个 RPM 包的文件都安装到哪里去了 
rpm -ql
# 查看依赖关系
rpm -qpR
# 查看 rpm 包信息
rpm -qpi foo-1.0.l.i386.rpm
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

## Mac 查看 CPU 型号

```bash
sysctl -n machdep.cpu.brand_string
system_profiler SPHardwareDataType
```

CPU 比较的网站：[CPU-Monkey](http://www.cpu-monkey.com)

## Git 仓库迁移

Clone 一份裸仓库

```bash
git clone --bare git@github.com/chrisniael/oldrepo.git
```

以镜像的方式上传到新 Git 服务器上

```bash
cd oldrepo
git push --mirror git@shenyu.me/chrisniael/newrepo.git
```

## CMake Release/Debug 编译

```bash
cmake -DCMAKE_BUILD_TYPE=Release .
cmake -DCMAKE_BUILD_TYPE=Debug .
```

## CentOS 7 防火墙操作

开放端口

```bash
firewall-cmd --zone=public --add-port=3000/tcp --permanent
firewall-cmd --reload
```

检查

```bash
firewall-cmd --list-all
firewall-cmd --state
```

## Git HTTP 协议记住密码

```bash
git config --global credential.helper store
```

## CentOS 7 Home 目录改为英文

```bash
export LANG=en_US
xdg-user-dirs-gtk-update
```

## 查看端口占用情况

```bash
netstat -anp | grep 80
```

## GNome Terminal 光标不闪烁

```bash
gsettings set org.gnome.desktop.interface cursor-blink false
```

## Vim 替换换行符

将 false\n 替换为 true\n

```vim
:%s/false\n/true\r/g
```

## 修改 Linux Firefox 的默认缩放比

在网址里输入 `about:config`，将字段 `layout.css.devPixelsPerPx` 改为 `1.2` 或更大。


## C++ 终端打印 wstring

```cpp
#include <iostream>
#include <locale>
#include <string>

std::wcout.sync_with_stdio(false);
std::wcout.imbue(std::locale("zh_CN.UTF-8"));

std::wstring wstr(L"今天");
std::wcout << std::endl;
```

## C++ 按行读取为 wstring

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <locale>
#include <cstdlib>

std::wifstream wif(filename);
wif.imbue(std::locale("zh_CN.UTF-8"));

std::wcout.imbue(std::locale("zh_CN.UTF-8"));
std::wstring wstr;
while(std::getline(wif, wstr))
{
    std::wcout << wstr << std::endl;
    std::wcout << wstr.size() << std::endl;
}
```

## CentOS 7 修改最大文件打开数

修改文件 `/etc/security/limits.conf`

```config
* soft nofile 65535
* hard nofile 65535
```

然后执行

```bash
ulimit -n 65535
```

## htpasswd 网站加密访问

生成密码文件

```bash
htpasswd -bc .passwd shenyu 123456
```

修改 nginx 配置

```config
auth_basic "project-name-auth";
auth_basic_user_file path/.htpasswd;
```

热更 nginx 配置

```bash
nginx -s reload
```

## Git 创建 tag

```bash
git tag 1.0
git tag -am "your comment text." 1.0
git tag
git show 1.0
git push origin 1.0
git push origin --tags
```

## Linux 卸载 Ruby 以及所有的 Ruby 组件

```bash
for x in `gem list --no-versions`; do gem uninstall $x -a -x -I; done
yum remove ruby
```

## 脚本中 export 环境变量到运行脚本的 Bash 中

```bash
source example.sh
```

## gem

```bash
# 更新 gem 自身
# 注意：在某些 Linux 发行版中为了系统稳定性此命令禁止执行
gem update --system

gem install gemname

gem install -l gemname.gem

gem install gemname --version=1.0

# 更新所有已安装的gem 包
gem update

# 更新指定的 gem 包
# 注意：gem update gemname 不会升级旧版本的包，此时你可以使用 gem install gemname --version=ver 代替
gem update gemname

# 删除指定的 gem 包，注意此命令将删除所有已安装的版本
gem uninstall gemname

# 删除某指定版本 gem 包
gem uninstall gemname --version=ver

# 查看本机已安装的所有 gem 包
gem list [--local]

gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/

gem sources -l
```

## C++ 创建一个不带缓冲区的文件流

```cpp
std::ifstream f;
f.rdbuf()->pubsetbuf(0, 0);
f.open("example.txt")
```

## Git Submodule

* clone 并初始化带 submodule 的仓库

    ```bash
    git clone --recursive git@shenyu.me:shenyu/example.git
    ```

    或者

    ```bash
    git clone git@shenyu.me:shenyu/example.git
    git submodule update --init --recursive
    ```
* 增加 submodule

    ```bash
    git submodule add git@shenyu.me:shenyu/submodule-a.git
    git submodule update --init --recursive
    git add .
    git commit -m "Add a module."
    git push origin master
    ```

    `git submodule add module-repo` 并不会 clone module 的子模块仓库，所以需要再执行 `git submodule update --init --recursive`。

* 更新 submodule

    ```bash
    git submodule update --init --remote --recursive
    git add .
    git commit -m "Update submodule."
    git push origin master
    ```
* 删除 submodule

    ```bash
    mv submodule submodule-backup
    git submodule deinit -f -- submodule
    rm -rf .git/modules/submodule
    git rm -f submodule
    git push origin
    ```
* 修改 submodule 仓库地址

    ```bash
    git submodule deinit -f -- submodule
    rm -rf .git/modules/submodule
    vim .gitmodule
    git submodule update --init --recursive
    git commit -m "Change "
    git push origin master
    ```

* 查看 submodule 状态

    ```bash
    git submodule status --recursive
    ```

## SELinux 增加删除 HTTP 端口

* 增加

    ```bash
    semanage port -a -t http_port_t -p tcp 888
    semanage port -l | grep http_port
    netstat -lpn —tcp | grep 888
    ```
* 删除
    ```bash
    semanage port -d -t http_port_t -p tcp 888
    semanage port -l | grep http_port
    ```

## Mac 终端发送 iMessage

```bash
osascript -e 'tell application "Messages" to send "我在用命令行发短信，哈哈哈" to buddy "老大"'
```

## CMake Visual Studio /MT 和 /MTd 选项

```cmake
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
```

## Windows Cmder Bash 右键打开直接进入对应目录

```bash
if [ -n "$CMDER_START" ]
then
    cd ${CMDER_START}
fi
```

## Windows Cmder 保持 SSH 连接

配置 ssh 客户端每 60 秒发包给服务器来保持连接

```config
Host *
    ServerAliveInterval 60
```

也可以指定域名，可以用通配符

```config
Host *hostname.com
    ServerAliveInterval 60
```

## 终端使用 HTTP 代理

Mac/Linux

```bash
export http_proxy=http://127.0.0.1:1087
export https_proxy=http://127.0.0.1:1087
```

Windows

```cmd
set http_proxy=http://127.0.0.1:1080
set https_proxy=http://127.0.0.1:1080
```

URL 是本地 HTTP 代理监听的地址。

## Visual Studio 注释代码快捷键

* Ctrl-K + Ctrl-C : 注释选择的代码
* Ctrl-K + Ctrl-U : 取消注释选择的代码

## CentOS 7 关闭 SELinux

```config
#/etc/sysconfig/selinux

SELINUX=disabled
```

```bash
setenforce 0
getendorce
```

## SElinux 导致 SSH authorized_keys 不生效

查看日志 `/var/log/audit/audit.log`

```bash
restorecon -R -v /root/.ssh
```

[Setting up SSH authorized_keys with SELinux enabled](https://www.pyrosoft.co.uk/blog/2013/01/12/setting-up-ssh-authorized_keys-with-selinux-enabled/)

## SSH 强制踢用户下线

```bash
w
who am i
pkill -kill -t pts/1
```

## Mac SSH Client 保持连接

`vim ~/.ssh/config`

``` bash
ServerAliveInterval 30
ServerAliveCountMax 60
```

## Linux 性能分析工具 perf

```bash
perf top -p pid
```

## Linux 清理内存

```bash
echo 1 > /proc/sys/vm/drop_caches
```

## Top 查看指定进程各个线程状态

```bash
Top -Hp pid
```

## 查看端口占用情况

```bash
netstate -anpt | grep 80
```

## Linux 查看二进制文件依赖的动态库

```bash
ldd bin
```

## Gcc 关闭返回值优化

```
g++ -fno-elide-constructors main.cpp -o main
```

## 读取文件的 16 进制内容

```bash
xxd file
xxd file file-out
xxd -r file-out
```

还可以组合 Vim 进行操作，Vim 以二进制方式打开 `vim -b`

```vim
:%!xxd file
```

还可以直接用 Vim 以二进制打开一个文件进行操作

```vim
:%!xxd
```

```vim
:%!xxd -r
```

## Vim -b 作用

以二进制方式打开文件，不会在末尾自动加上换行符。

```bash
echo -n "test vim -b command." > test.txt
cat test.txt
vim test.txt    // 保存并退出
cat test.txt
```
执行完后文件 test.txt 末尾多加一个换行符。

```bash
echo -n "test vim -b command." > test.txt
cat test.txt
vim -b test.txt
cat test.txt
```

而用 `vim -b` 方式打开则不会出现这个问题。

## Linux 网络流量监控 iptraf-ng

```bash
yum install iptraf-ng
```

## Ubuntu 软件包安装相关

```bash
apt-cache searh <pkg>    # 搜索
apt-cache show <pkg>     # 查看详细信息
apt-get install <pkg>    # 安装
dpkg -L <pkg>            # 查看包安装了哪些文件
```

## Yum 加快下载速度

可以先开代理，然后

```bash
yum makecache fast
```

## Git 远程已经删除的分支

```bash
git remote show origin
git remote prune origin
```

## SSH 关闭密码登陆

```bash
vim /etc/ssh/sshd_config
```

```
PasswordAuthentication no
```

## Docker 容器开机自动启动

```basa
docker run --restart=always <image>
```

可以修改已经启动的容器的属性

```bash
docker container update --restart=always <container>
```
