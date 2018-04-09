# Windows-Server-2012

###Windows Server 2012通过计算机管理添加用户和组  
通过win+R打开运行窗口，输入```compmgmt.msc```  
###修改远程桌面3389端口批处理
```@echo off
color f0
echo 修改远程桌面3389端口(支持Windows 2003 2008 2008R2 2012 2012R2 7 8 10 )
echo 自动添加防火墙规则
echo %date%   %time%
echo    ARK 
set /p c= 请输入新的端口:
if "%c%"=="" goto end
goto edit
:edit
netsh advfirewall firewall add rule name="Remote PortNumber" dir=in action=allow protocol=TCP localport="%c%"
netsh advfirewall firewall add rule name="Remote PortNumber" dir=in action=allow protocol=TCP localport="%c%"
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp" /v "PortNumber" /t REG_DWORD /d "%c%" /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v "PortNumber" /t REG_DWORD /d "%c%" /f
echo 修改成功
echo 重启后生效，按任意键重启
pause
shutdown /r /t 0
exit
:end
echo 修改失败
pause  


# Windows10 install WSL
### 步骤  
我们先要启用适用于 Linux 的 Windows 子系统。以 管理员 身份运行 Powershell，输入以下内容。完成后按 Y 重启电脑。  
`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`  
或者可以在 控制面板 > 程序 > 启用或关闭 Windows 功能 中，勾选“适用于 Linux 的 Windows 子系统(Beta)”，然后点确定。根据提示重启。
重启以后，启用开发人员模式。以 管理员 身份运行 Powershell，输入以下内容：
`reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\AppModelUnlock" /t REG_DWORD /f /v "AllowDevelopmentWithoutDevLicense" /d "1"`  
或者可以在 设置 > 更新和安全 > 针对开发人员 中，选择 “开发人员模式”  
最后安装 Ubuntu，建议用 非管理员 模式运行 Powershell，输入以下内容。完成安装之后，输入 bash 进入 Ubuntu 系统。  
`lxrun /install /y`  
