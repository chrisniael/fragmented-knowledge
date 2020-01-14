# Wox 配置

## 依赖

* .net framework >= 4.5.2
* [everything](https://www.voidtools.com), 64 bit 操作系统安装 64 bit 版本
* [python3](https://www.python.org/downloads/windows), 64 bit 操作系统安装 64 bit 版本

## 设置

#### 通用

* 开机自动启动
* 失去焦点时自动隐藏 Wox
* 隐藏任务栏图标 (隐藏后可以输入 settings 呼出)
* 语言：中文
* 上一次搜索关键字模式：全选上一次关键字

    这块有 bug，暂时的解决方案：使用 Windows 7 兼容性模式运行，要设置 2 个地方
    * 桌面 Wox 快捷方式 - 属性 - 兼容性 - 以兼容性模式运行这个程序 - Windows 7 
    * 任务管理器 - 启动 - Wox - 属性 - 兼容性 - 以兼容性模式运行这个程序 - Windows 7
* python path

    add it to %PATH% or set it in WoX settings

#### 插件

* 网页搜索
    * google
    * github
    * translate
    * wikipedia
    * youtube
    * jd
      * https://search.jd.com/Search?keyword={q}&enc=utf-8&wq={q}
    * suning
      * https://search.suning.com/{q}/
    * taobao
      * https://s.taobao.com/search?q={q}&imgfile=&commend=all&search_type=item&sourceId=tb.index&ie=utf8
    * amazon
      * https://www.amazon.cn/s?k={q}
* 命令行
    * 替换 Win + R
    * PowerShell

#### 热键

Alt + Space
