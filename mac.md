# Mac

## ldd in macOS

Mac 上显示二进制文件使用的动态库 (Linux ldd 的功能)

```bash
otool -L <binary-file>
```

## 快速显示词典释义

1. 选择文字后，触发键盘快捷键

   ```bash
   CMD + CTRL + D
   ```

2. 触摸板三指轻触选择的文字 (默认是 "单指用力点按")

   系统偏好设置 - 触摸板 - 光标与点按 - 查询与数据监测器
   选择 "三个手指轻点"

3. 自定义快捷键

   系统偏好设置 - 键盘 - 快捷键 - 服务 - 在词典中查询
   勾选并设置自定义快捷键

<https://medium.com/@hlung/how-to-quickly-look-up-a-word-in-dictionary-mac-os-x-ef500d6cbdd>

## 查看端口占用

```bash
lsof -nP -iTCP:1080 -sTCP:LISTEN  # TCP, 1080 端口, LISTEN 状态的进程
lsof -nP -iTCP -sTCP:LISTEN       # TCP, LISTEN 状态的进程
lsof -nP -i:1080 -sTCP:LISTEN     # 1080 端口，LISTEN 状态的进程
```
