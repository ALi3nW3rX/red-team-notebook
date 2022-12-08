# Spidering Shares

Options for spidering shares of remote systems. Example, Spider the C drive for files with txt in the name (finds both sometxtfile.html and somefile.txt)

Notice the '$' character has to be escaped. (example shown can be used as-is in a kali linux terminal)

```
#~ cme SMB <IP> -u USER -p PASSWORD --spider C\$ --pattern txt
```

## Using module Spider\_plus

The module `spider_plus` allows you to list and dump all files from all readable shares thanks to [@vincd](https://github.com/vincd)

### List all readable files

```
crackmapexec smb 10.10.10.10 -u 'user' -p 'pass' -M spider_plus
```

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

### Dump all files

Using the option `-o READ_ONLY=false` all files will be copied on the host

```
crackmapexec smb 10.10.10.10 -u 'user' -p 'pass' -M spider_plus -o READ_ONLY=false
```

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>
