# Null Sessions

Checking if **Null Session** is enabled on the network, can be very useful on a Domain Controller to enumerate users, groups, password policy etc

```
#~ cme smb 10.10.10.161 -u '' -p ''
#~ cme smb 10.10.10.161 --pass-pol
#~ cme smb 10.10.10.161 --users
#~ cme smb 10.10.10.161 --groups
```

<figure><img src="../../../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

You can also reproduce this behavior with `smbclient` or `rpcclient`

```
smbclient -N -U "" -L \\10.10.10.161
```

```
rpcclient -N -U "" -L \\10.10.10.161
rpcclient $> enumdomusers
user:[bonclay] rid:[0x46e]
user:[zoro] rid:[0x46f]

```

### Example

Forest or Monteverde machines are good examples to test **null session** authentication with CrackMapExec

{% embed url="https://www.hackthebox.eu/home/machines/profile/212" %}

{% embed url="https://www.hackthebox.eu/home/machines/profile/223" %}

