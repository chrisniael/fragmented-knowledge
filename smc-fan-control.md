# Smc Fan Control

<https://github.com/hholtmann/smcFanControl/tree/master/smc-command>

写操作需要 root 权限，读不用。

*  显示当前设置的信息, 取所有风扇 ID

    ```
    ./smc -f
    ```
* 取 Mx 值作为最发风扇转速

    ```bash
    ./smc -k F0Mx -r
    ```
* 强制模式(手动控制速度), 01: 强制模式, 00: 自动模式

    ```bash
    sudo ./smc -k F0Md -w 01
    ```
* 指定目标风扇速度, 编码方式还不知

    ```bash
    sudo ./smc -k F0Tg -w 00808945
    ```
* 显示所有传感器温度

    ```bash
    ./smc -t
    ```
