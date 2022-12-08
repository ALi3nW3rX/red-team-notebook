# BloodHound Integration

CrackMapExec will set user as 'owned' on BloodHound when an account is found ! Very usefull when lsassy finds 20 credentials in one dump :)

First you need to configure your config file in you home folder: `~/.cme/cme.conf` and add the following lines:

```
[BloodHound]
bh_enabled = True
bh_uri = 127.0.0.1
bh_port = 7687
bh_user = user
bh_pass = pass
```

Then, every time cme will find a valid credential, it will be added to bloodhound.

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>
