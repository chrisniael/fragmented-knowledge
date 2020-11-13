# Mac 登陆时不显示其他用户登陆选项

系统偏好设置 → 用户与群组 → 点按锁按钮解锁 → 客人用户 → 允许客人登陆这台电脑 (取消勾选)

按上面这样操作，如果还是显示，则可以在命令行执行下面操作：

```bash
sudo defaults write /Library/Preferences/com.apple.loginwindow SHOWOTHERUSERS_MANAGED -bool FALSE
```

<https://www.wdiaz.org/how-to-remove-guest-user-from-login-on-macos/>
