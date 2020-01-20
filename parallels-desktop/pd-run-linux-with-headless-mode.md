# Parallels Desktop 以 Headless 模式运行 Linux 

1. 配置 - 选项 - 启动和关机 - 始终在后在准备就绪
2. 通过 `prlctl` 命令启动 Linux 虚拟机

    ```bash
    prlctl list --all  # 显示所有 vm
    prlctl start <vm-name>
    prlctl list  # 显示启动着的 vm
    ```
    * https://stackoverflow.com/questions/17098927/how-do-i-run-ubuntu-server-headless-using-parallels-desktop
    * https://www.macissues.com/2016/01/03/how-to-run-headless-virtual-machines-in-os-x/
