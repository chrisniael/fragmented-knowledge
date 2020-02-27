# Curl

## -f, --fail

当 HTTP 服务器失败时（response code 是 4xx），通常情况下会返回一个描述为什么出错的 HTML 的文档。这个参数会阻止 curl 输出这个 HTML 文档，并且设置 curl 的返回值为 22。

这个方法并不能完全检测到 response code 失败的情况 (not fail-safe)，可能会存在漏网之鱼，特别是引入了 authentication (response code 401 和 407) 的时候。

## -L, --location

当 HTTP response code 是 3xx 时，curl 会重新请求新的地址。

## -S, --show-error

当和 -s, --silent 一起使用时，curl 会在出错时显示错误信息。

## -s, --silent

不显示下载进度条和错误信息。

当和 -S, --show-error 一起使用时可以关闭下载进度条但是显示错误信息。

## --request, -X <comman>

HTTP 请求的方法。

## -d, --data <data>

请求方法会被设置为 `POST`。

`Content-Type` 会被设置成 `application/x-www-form-urlencoded`。

如果 `<data>` 以 `@` 开头，则后面必须跟上一个文件名，curl 会读取这个文件内容作为 `POST` 的 body。

会去除 `\r`, `\n`。

如果在一个命令行语句里多次使用了这个选项，则这些数据会被合并在一起且用 `&` 分隔。所以，`-d name=daniel -d skill=lousy` 会被处理为 `name=daniel&skill=lousy`。

## --data-ascii <data>

参数 `-d`, `--data` 的别名。

## --data-binary <data>

与 `-d`, `--data` 功能一致，但是不会去除 `\r`, `\n`。

## --data-raw <data>

与 `-d`, `--data` 功能一致，除了不支持使用 `@` 字符来指定文件来作为 POST 内容。

4.43.0 才加入的参数。

## --data-urlencode <data>

与 `-d`, `--data` 功能一致，但是还会对 `<data>` 内容进行 URL-encoding。
