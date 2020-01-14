# 下一个 pane 快捷键

prefix o: Select the next pane in the current window

prefix C-o: Rotate the panes in the current window forwards.

当 prefix 设置成 Ctrl + j 时，很容易在想按 prefix o 时误触 prefix C-o，索性把 prefix C-o 也映射成 prefix o 的功能

```conf
unbind C-o
bind C-o select-pane -t :.+
```
