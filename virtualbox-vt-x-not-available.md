# VirtualBox VT-x is not available (VERR_VMX_NO_VMX)

确保 BIOS 的 VT-x 已开启。

1. 以管理员身份运行 CMD

2. 执行下面命令

   ```cmd
   bcdedit
   ```

   `hypervisorlaunchtype` 属性的值默认应该是 `Auto`。

3. 修改 hypervisorlaunchtype 的值为 off

   ```cmd
   bcdedit /set hypervisorlaunchtype off
   ```

4. 重启电脑

[https://forums.virtualbox.org/viewtopic.php?f=38&t=89791](https://forums.virtualbox.org/viewtopic.php?f=38&t=89791)
