# Kindle

探讨 Kindle 生态对 azw3、epub、mobi 和 pdf 格式文档的支持情况。

## 封面显示问题

* Amazon 购买
* mobi 7 使用邮件发送至 Kindle
* mobi 8 使用 USB 导入至 Kindle
* azw3 使用 USB 导入至 Kindle

<https://zhuanlan.zhihu.com/p/77413845>

## 二级目录显示问题

Kindle 处理 mobi 7 格式文档时，二级目录不能显示不正常（没有缩进），这个不是格式本身的问题，而是 Kindle 阅读器本身支持不好的原因，换其他阅读器软件是好的。

## 格式支持

* Amazon 电子书购买

    Amazon 购买的电子书都支持。

* Kindle 邮件导入

    不支持 epub 和 azw3 格式，支持 mobi 和 pdf。

* Kindle USB 导入

    不支持 epub 格式，支持 azw3、mobi 和 pdf。

## 云端书签

Amazon 购买的电子书肯定能在云端存储书签，还有就是通过能邮件导入 Kindle 的文档（mobi）也支持云端存储书签，pdf 格式除外。azw3 本来就不支持通过邮件导入 Kindle，就不用想这个功能了。

云端书签还支持导出功能，Amazon 购买的电子书可以通过邮件导出 csv 和 pdf 格式存储的书签记录。通过邮件导入 Kindle 的文档也而可以通过邮件的方式导出书签，但存储格式是 html 的。

## 支持清单

v : 支持
x : 不支持
o : 没有这个选项

| 文件类型 | 导入方式    | 正常阅读 | 封面显示 | 二级目录显示 | 未下载前封面显示 | 书签云端同步 | 书签邮件导出 |
|----------|-------------|----------|----------|--------------|------------------|--------------|--------------|
| azw3     | Amazon 购买 | v        | v        | v            | v                | v            | v (csv, pdf) |
| epub     | 邮件        | x        | x        | x            | x                | x            | x            |
| azw3     | 邮件        | x        | x        | x            | x                | x            | x            |
| mobi 8   | 邮件        | v        | x        | v            | x                | v            | v (html)     |
| mobi 7   | 邮件        | v        | v        | x            | x                | v            | v (html)     |
| pdf      | 邮件        | v        | x        |              |                  | x            | x            |
| epub     | USB         | x        | x        | x            | x                | x            | x            |
| azw3     | USB         | v        | v        | v            | o                | x            | x            |
| mobi 8   | USB         | v        | x        | v            | o                | x            | x            |
| mobi 7   | USB         | v        | v        | x            | o                | x            | x            |
| pdf      | USB         | v        | x        |              | o                | x            | x            |

综上，对于 Kindle 生态，Amazon 购买的电子书体验自然是最好的，非 Amazon 购买的文档，mobi 7 是比较好的选择。
