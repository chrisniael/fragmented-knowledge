# OpenWrt

## 编译

```bash
./scripts/feeds clean
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
make -j1 V=s
```

`V=s` : 表示编译的时候显示日志输出，方便出错的时候查错。

https://stackoverflow.com/a/25599194/6354155


## Passwall 插件

将下面的内容添加到 `feeds.conf.default` 文件中。

```config
# feeds.conf.default
# ...
src-git lienol https://github.com/Lienol/openwrt-package
```

然后再编译。


## 中文支持

```
opkg install luci-i18n-base-zh-cn
```

也可以在编译的时候就安装中文语言包。

## WEB 管理界面报错

```log
/usr/lib/lua/luci/model/cbi/passwall/api/v2ray.lua:6: module 'luci.model.ipkg' not found:
...
```

编译时选择 `luci-lib-ipkg` 组件

https://github.com/Lienol/openwrt-package/issues/77
