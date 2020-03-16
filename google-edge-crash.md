# Google/Edge Crash After Update

电脑安装了 Symantec Endpoint Protection，Chrome 和 Edge 打开网页都不能正常使用，且插件也都无法正常加载。

Google 在 Chrome 78 中引入了 Windows 10 特有的 "renderer code integrity" 功能，该功能目的在于防止未签名的代码 (病毒等) 控制 Chrome 的页面渲染过程。可笑的是某些杀毒软件也会将自己未签名的代码注入 Chrome，以便监控网络流量，防止用户浏览恶意的网站。一般是通过 DLL 注入每个 chrome.exe 的进程完成的。

有下面几种几种解决方案，都是通过关闭 Chrome 的 "renderer code integrity" 功能完成的。

## 方法一

在 Chrome/Edge 的桌面快捷方式后增加参数 `--disable-features=RendererCodeIntegrity`

```
"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --disable-features=RendererCodeIntegrity
"C:\Program Files (x86)\Microsoft\Edge\Application\msedge.exe" --disable-features=RendererCodeIntegrity
```

然后每次启动都通过这个桌面快捷方式启动，从开始菜单启动还是会崩溃。


## 方法二 (推荐)

通过管理员身份打开 CMD，然后执行下面这段命令

```cmd
reg add "HKEY_LOCAL_MACHINE\Software\Policies\Google\Chrome" /v RendererCodeIntegrityEnabled /t REG_DWORD /d 0 /f
reg add "HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Edge" /v RendererCodeIntegrityEnabled /t REG_DWORD /d 0 /f
```

这样无论从开始菜单，还是从桌面快捷方式都可以正常启动 Chrome/Edge。

## 参考

* https://9to5google.com/2019/10/29/google-chrome-78-aw-snap-crash-windows/
* https://docs.microsoft.com/en-us/deployedge/microsoft-edge-policies#renderercodeintegrityenabled
