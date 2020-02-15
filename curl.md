# Curl

## -f, --fail

当 HTTP 服务器失败时（response code 是 4xx），通常情况下会返回一个描述为什么出错的 HTML 的文档。这个参数会阻止 curl 输出这个 HTML 文档，并且设置 curl 的返回值为 22。

这个方法并不能完全检测到 response code 失败的情况 (not fail-safe)，可能会存在漏网之鱼，特别是引入了 authentication (response code 401 和 407) 的时候。

## -L, --location

当 HTTP response code 是 3xx 时，curl 会重新请求新的地址。
