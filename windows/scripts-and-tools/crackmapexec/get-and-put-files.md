# Get and Put Files

Send a local file to the remote target

```
#~ cme smb 172.16.251.152 -u user -p pass --put-file /tmp/whoami.txt \\Windows\\Temp\\whoami.txt
```

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

## Get a file from the remote target

Get a remote file on the remote target

```
#~ cme smb 172.16.251.152 -u user -p pass --get-file  \\Windows\\Temp\\whoami.txt /tmp/whoami.txt
```

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

