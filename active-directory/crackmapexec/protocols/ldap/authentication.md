# Authentication

Testing if account exist without kerberos protocol

```
#~ cme ldap 192.168.1.0/24 -u users.txt -p '' -k
```

<figure><img src="../../../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

#### Testing credentials

```
#~ cme ldap 192.168.1.0/24 -u user -p password
```

```
#~ cme ldap 192.168.1.0/24 -u user -H A29F7623FD11550DEF0192DE9246F46B
```

Expected Results:

```
LDAP        192.168.255.131 5985   ROGER            [+] GOLD\user:password
```

{% hint style="warning" %}
Domain name resolution is expected
{% endhint %}

By default, the ldap protocol will ge the domain name by making connection to the SMB share (of the dc), if you don't want that initial connection, just add the option `--no-smb`
