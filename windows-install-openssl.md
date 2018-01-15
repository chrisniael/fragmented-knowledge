# Windows 安装 OpenSSL

## 环境安装

1. Visual Studio Community 2017
    下载地址：[https://www.visualstudio.com/zh-hans/downloads](https://www.visualstudio.com/zh-hans/downloads)
2. ActivePerl
    下载地址：[https://www.activestate.com/activeperl/downloads](https://www.activestate.com/activeperl/downloads)
3. Nasm 汇编器
    下载地址：[http://www.nasm.us](http://www.nasm.us)
4. OpenSSL 源码
    下载地址：[http://www.openssl.org](http://www.openssl.org)
    不要使用 Github 上的 OpenSSL 仓库的代码。

## 编译 OpenSSL

1. 打开 cmd，配置编译环境

    编译 Win32：

    ```cmd
    cd C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build
    vcvars32.bat
    ```

    编译 Win64：

    ```cmd
    cd C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Auxiliary\Build
    vcvars64.bat
    ```

    这边也可以直接打开 `x86 Native Tools Command Prompt for VS 2017` 或 `x64 Native Tools Command Prompt for VS 2017` 程序，不用执行批处理来配置环境，分别对应编译 Win32 和 Win64 平台。

2. 解压下载下来的 OpenSSL 源码，进入解压后的目录

    ```cmd
    cd openssl-1.0.2n
    ```
3. 配置编译文件和安装目录

    编译 Win32：

    ```cmd
    perl Configure VC-WIN32 --prefix=C:\openssl
    ```

    编译 Win64：

    ```cmd
    perl Configure VC-WIN64A --prefix=C:\openssl
    ```
4. 搭建编译环境

    编译 Win32：

    ```cmd
    ms\do_nasm
    ms\do_ms
    ```
    编译 Win64：

    ```cmd
    ms\do_nasm
    ms\do_win64a
    ```
5. 编译 OpenSSL

    ```cmd
    nmake -f ms\ntdll.mak
    ```
6. 安装编译的库

    ```cmd
    nmake -f ms\ntdll.mak install
    ```

## 参考资料

[如何在 Windows 下编译 OpenSSL (intel.com)](https://software.intel.com/zh-cn/blogs/2013/12/22/windows-openssl)
