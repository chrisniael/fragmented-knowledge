# 检测是否以管理员身份运行

```bat
rem 测试是否有管理员权限
rd "%WinDir%\system32\test_permissions" >nul 2>nul
md "%WinDir%\System32\test_permissions" 2>nul || (echo 请右击以管理员身份运行！&& pause >nul && exit)
rd "%WinDir%\System32\test_permissions" 2>nul
```

* %WinDir% : `C:\Windows`

只有管理员才有权限在目录 `C:\Windows\System32` 新建目录，以此来检测脚本是否以管理员身份运行。
