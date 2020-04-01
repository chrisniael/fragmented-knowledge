# Windows 一些使用技巧


## 自定义启动程序目录

#### For current user

C:\Users\Username\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

win + r
shell:startup


#### For all user

C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp

win + r
shell:common startup


## 开始菜单程序

shell:common programs
shell:programs

## 关闭 CMD 提示音

以管理员身份打开 CMD，执行

```cmd
sc config beep start= disabled
sc stop beep
```

## 关闭 UAC 提示音 

控制面板 - 硬件和声音 - 更改系统声音

将 **Windows 用户账户控制** 这个程序事件的声音设置成 **(无)**

## 关闭 Windows 开始菜单对目录文件的搜索

控制面板 - 索引选项 - 修改

去除所有目录

控制面板 - 索引选项 - 高级 - 索引设置 - 疑难解答 - 删除和重建索引 - 重建

## 重置 thumbnailcache

以管理员身份打开 CMD，执行

```cmd
taskkill /f /im explorer.exe
del /f /s /q /a %LocalAppData%\Microsoft\Windows\Explorer\thumbcache_*.db
start explorer.exe
```

## 重建 iconcache

以管理员身份打开 CMD，执行

```cmd
taskkill /f /im explorer.exe
del /f /s /q /a %LocalAppData%\IconCache.db
del /f /s /q /a %LocalAppData%\Microsoft\Windows\Explorer\iconcache_*.db
start explorer.exe
```

## 查看端口占用

```cmd
netstat -ano | findstr "1080"
```
最后一列是进程的 PID

## 查看 PID 进程名

```cmd
tasklist | findstr "9088"
```

## 结束 PID 进程

```cmd
taskkill /t /f /pid 9088 
```
