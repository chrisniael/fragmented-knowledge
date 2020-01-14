# tmux 重新加载配置时忽略 powerline-daemon 返回值

```conf
run-shell "powerline-daemon -q || true"
source /usr/lib/python3.8/site-packages/powerline/bindings/tmux/powerline.conf
```
