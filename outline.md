# Outline

* 关闭服务器防火墙，或者设置入口流量允许所有端口通过。
* 安装 Outline Server。

    ```bash
    wget -qO- https://raw.githubusercontent.com/Jigsaw-Code/outline-server/master/src/server_manager/install_scripts/install_server.sh | bash
    ```
* 复制 json 字符串至 Outline Manager 客户端中。
* 使用 Outline Client 客户端连接 Shadowsocks 服务 ，或者直接用 Shadowsocks 客户端。
