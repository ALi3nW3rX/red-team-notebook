# Anonymous Login



Using a random username and password you can check if the target accepts annonymous logon

{% hint style="danger" %}
Make sure the password is empty&#x20;
{% endhint %}

```
cme smb 10.10.10.178 -u 'a' -p ''
```

<figure><img src="../../../../.gitbook/assets/image (43) (1).png" alt=""><figcaption></figcaption></figure>

You can also check this **** behavior with **smbclient** or **rpcclient**

```
smbclient -N -L \\10.10.10.178
rpcclient -N -L 10.10.10.178
```
