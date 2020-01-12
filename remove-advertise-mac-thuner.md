# Mac 迅雷去除广告

* advertising.xlplugin : 底部广告文字链接
* applications.xlplugin : 应用标签（删除后副作用就是不能进入设置页面）
* featuredpage.xlplugin : 精选标签
* liveupdate.xlplugin : 在线插件（一定要删除这个，否则广告插件 advertising.xlplugin 会自动更新在本地）


```bash
rm -rf /Users/shenyu/Library/Application Support/Thunder/PlugIns
```
这个目录缓存了插件 viptask.xlplugin、 xlbrowser.xlplugin、 advertising.xlplugin 
