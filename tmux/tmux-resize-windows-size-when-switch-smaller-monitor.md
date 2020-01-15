# 切换到小屏幕后 tmux 重新调整窗口大小

## 方法一

```bash
tmux attach -d
```

-d : detach other clients attached to target session

tmux 默认会使用最小的 client 大小来显示 session 窗口，只要把其他 client 剔除，就可以重新调整大小了

* https://stackoverflow.com/a/7819465


## 方法二

在 tmux 里执行

```
prefix shift d
```

* https://stackoverflow.com/a/22184685
