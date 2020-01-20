# xsel 进程不会自动退出

## 原因

```bash
man xsel
```

```text
There is no X selection buffer. The selection mechanism in X11 is an interclient communication mediated by the X server each time any program wishes to  know  the  selection contents,  eg.  to perform a middle mouse button paste. In order to implement modification of the selection(s) (in input, keep and exchange modes) this program detaches from the terminal, spawning a child process to supply the new selection(s) on demand. This child exits immediately when any other program takes over the  selection(s),  eg.  when the user next selects some text in a terminal window or by running xsel -c.
```

## 解决方案

#### ssh

```bash
# ~/.zshrc
alias exit="xsel -c && exit"
```

#### tmux

```config
# ~/.tmux.conf
bind d run-shell "xsel -c && tmux detach -P"
```

## 参考

* https://stackoverflow.com/a/19260314
