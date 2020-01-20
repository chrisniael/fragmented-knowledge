# Detect return value of cmd

bat 脚本里可以通过 `%RETURNVALUE%` 获取上一条命令的返回值，在交互式命令行跑完全没有问题，但是放在脚本文件里执行，就是取不到正确的值。

## 解决方案

```bat
setlocal EnableDelayedExpansion

echo !RETURNVALUE!
```


## 参考

* https://stackoverflow.com/a/9935813
* https://www.jb51.net/article/29323.htm
