# Authentication



### WinRM Authentication

#### Testing credentials

```
#~ cme winrm 192.168.1.0/24 -u user -p password
```

Expected Results:

```
WINRM       192.168.255.131 5985   ROGER            [*] http://192.168.255.131:5985/wsman
WINRM       192.168.255.131 5985   ROGER            [+] GOLD\user:password (Pwn3d!)
```

If the SMB port is closed you can also use the flag `-d DOMAIN` to avoid an SMB connection

```
#~ cme winrm 192.168.1.0/24 -u user -p password -d DOMAIN
```

Expected Results:

```
WINRM       192.168.255.131 5985   192.168.255.131  [*] http://192.168.255.131:5985/wsman
WINRM       192.168.255.131 5985   192.168.255.131  [+] GOLD\user:password (Pwn3d!)
```
