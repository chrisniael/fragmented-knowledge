# 一键 detach tmux 和 退出 ssh/shell

```bash
tmux detach -P
```

推荐重新定义 tmux d 快捷键

```conf
bind d detach -P
```

或者

`Enter` `~` `.` （putty 不支持）


* https://unix.stackexchange.com/questions/546820/detach-from-tmux-session-and-close-ssh-session-with-1-command
* https://unix.stackexchange.com/questions/41682/exit-out-of-all-ssh-connections-in-one-command-and-close-putty
* https://www.chiark.greenend.org.uk/~sgtatham/putty/wishlist/break-key.html
