<header><h2 align="center">惠普暗影精灵II Pro Win10修改记录</h2></header>

[TOC]

### Shadowsocks 修改注册表项

1. HKEY_USERS\S-1-5-21-1593614527-2614432062-2501410994-1001\Software\Microsoft\Windows\CurrentVersion\Internet Settings - [ProxyServer]
2. HKEY_USERS\S-1-5-21-1593614527-2614432062-2501410994-1001\Software\Microsoft\Windows\CurrentVersion\Internet Settings - [AutoConfigURL] (http://127.0.0.1:1080/pac?t=201605192324183352)
3. HKEY_USERS\S-1-5-21-1593614527-2614432062-2501410994-1001\Software\Microsoft\Windows\CurrentVersion\Internet Settings - [AutoConfigURL] (http://127.0.0.1:1080/pac?t=201605192324183352)

## 增加任务栏透明度时修改注册表项

在"HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced"增加了名称为"UseOLEDTaskbarTransparency"的项，其值为1