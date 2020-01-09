KiTTY Session Manager Build

## 中文显示乱码 bug 处理

* https://stackoverflow.com/questions/4967051/why-cant-i-find-or-use-urlencode-in-visual-studio-2010
* https://www.cnblogs.com/wang726zq/archive/2012/11/01/unicode.html

## Visual Studio 2010 (编译)

* 打开 Visual Studio 命令提示(2010)
* 执行

    ```bat
    buildrelease.bat
    ```

## NSIS (打包)

* 下载 2.46 版本（别下载最新版本，不兼容）

    https://sourceforge.net/projects/nsis/files/NSIS%202/2.46/
* 添加 killProcDLL 插件

    * https://stackoverflow.com/questions/25399569/invalid-command-killprocdllkillproc-nsi
    * https://nsis.sourceforge.io/KillProcDLL_plug-in
* 打包

    打开 cmd，执行
    ```bat
    compileinstaller.bat
    ```
