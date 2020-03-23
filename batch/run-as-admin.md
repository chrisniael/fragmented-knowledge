# 以管理员身份运行

```bat
@echo off

rem 使用管理员身份运行
cd /d "%~dp0"
cacls.exe "%SystemDrive%\System Volume Information" >nul 2>nul
if %errorlevel%==0 goto Admin
if exist "%temp%\getadmin.vbs" del /f /q "%temp%\getadmin.vbs"
echo Set RequestUAC = CreateObject^("Shell.Application"^)>"%temp%\getadmin.vbs"
echo RequestUAC.ShellExecute "%~s0","","","runas",1 >>"%temp%\getadmin.vbs"
echo WScript.Quit >>"%temp%\getadmin.vbs"
"%temp%\getadmin.vbs" /f
if exist "%temp%\getadmin.vbs" del /f /q "%temp%\getadmin.vbs"
exit

:Admin

rem 下面写要执行的代码
rem ...
```

假设当前 bat 文件路径是 `D:\path\to\myscript.bat`

* %~dp0 : 当前脚本所在的目录 (D:\path\to)
* %~s0 : 当前脚本文件路径名 (D:\path\to\myscript.bat)
* %temp%: 用户目录的 `AppData\Local\Temp` 目录

上面这段代码会生成一个 VB 文件：`%temp%\getadmin.vbs`，然后执行这个 VB 文件。

```vb
Set RequestUAC = CreateObject("Shell.Application")
RequestUAC.ShellExecute "D:\yourscript.bat","","","runas",1
WScript.Quit
```

这个 VB 代码会使用管理员身份调用 bat 脚本 (D:\path\to\myscript.bat)。
