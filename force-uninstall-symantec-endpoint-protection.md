# 强制删除 Symantec Endpoint Protection

1. 进入安全模式禁用 Symantec Endpoint Protection 服务

    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services`

    禁用下面这些服务，Start 项值修改为 4

    * SepMasterService: Symantec Endpoint Protection
    * SmcService:  SMC.exe, Symantec Management Client
    * SNAc: snac.exe, Symantec Network Access Control

2. Geek Uninstaller 强制卸载 Symantec Endpoint Protection
