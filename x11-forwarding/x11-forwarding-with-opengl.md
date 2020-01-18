# X11 Fording Works With OpenGL

## X Server enable ##Indirect GLX##

* Windows VcXsrv 默认是开启的
* Mac XQuartz 默认是关闭的

    ```bash
    defaults write org.macosforge.xquartz.X11 enable_iglx -bool true
    ```
    https://it.stonybrook.edu/help/kb/how-to-use-x11-tunnelling-with-interactive-jobs

## Client Run With Indrect Mode

```bash
export LIBGL_DEBUG=verbose
export LIBGL_ALWAYS_SOFTWARE=1
```

测试 OpenGL

```bash
pacman -S mesa-demos
LIBGL_DEBUG=verbose LIBGL_ALWAYS_SOFTWARE=1 glxgear
```

* https://www.scm.com/doc/Installation/Remote_GUI.html
* https://evpo.wordpress.com/2017/03/04/opengl-hardware-acceleration-through-remote-x11-ssh-connection/
