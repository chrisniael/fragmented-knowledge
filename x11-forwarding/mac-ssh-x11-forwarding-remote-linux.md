# Mac X11 Forwarding To Remote Linux

## 参考


## XQuartz 设置

#### 启动式不打开 xterm 终端

```bash
defaults read org.macosforge.xquartz.X11 app_to_run
```

默认值：/opt/X11/bin/xterm

```bash
defaults write org.macosforge.xquartz.X11 app_to_run /usr/bin/true
```

* https://apple.stackexchange.com/a/53737
* https://www.xquartz.org/FAQs.html


#### 同步 Remote Linux 粘贴板

勾选下面这三个

* 偏好设置 - 粘贴板 - 启用同步 √
* 偏好设置 - 粘贴板 - 启用同步 - CLIPBOARD √
* 偏好设置 - 粘贴板 - 启用同步 - 选定新文本时立即更新粘贴板 √

关于 clipboard, primary 可以参考：https://wiki.archlinux.org/index.php/Clipboard

* https://gist.github.com/benjaminhawkeslewis/2623263

#### Warning: No xauth data; using fake authentication data for X11 forwarding

环境变量 DISPLAY 不需要在 .zshrc 中手动设置，xquartz.startx 服务默认会自动给设置，xquartz.startx 服务默认是开启的

可以不使用 `-Y` 参数来登陆（不推荐）

```bash
SSH -X user@host  # without -XY
```

输出 ssh 登陆时调试信息，查看问题所在

```bash
ssh -XY -v user@host
```

可能是没有指定客户端的 xauth 路径

```config
# ~/.ssh/config
Host *
    XAuthLocation /opt/X11/bin/xauth
```

* https://serverfault.com/a/657996
* https://www.xquartz.org/FAQs.html


#### Enable Indirect GLX

```bash
defaults write org.macosforge.xquartz.X11 enable_iglx -bool true
```

* https://it.stonybrook.edu/help/kb/how-to-use-x11-tunnelling-with-interactive-jobs

#### 开机自动启动

系统偏好设置 - 用户与群组 - 登陆项 - + - 选择 XQuartz

* https://stackoverflow.com/a/43807922
