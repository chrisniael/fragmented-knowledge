KiTTY Session Manager Build

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
