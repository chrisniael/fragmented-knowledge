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
