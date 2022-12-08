# SMBCLIENT

#### <mark style="color:green;">SMB Enumeration</mark>

```
smbclient -N -L \\\\10.129.42.253
```

#### <mark style="color:green;">SMB Login</mark>

```
smbclient \\\\10.129.42.253\\share
```

#### <mark style="color:green;">SMB Login with User Creds</mark>

```
smbclient -U BOB \\\\10.129.42.253\\share
```

#### <mark style="color:green;">Get an entire directory</mark>

```
smbclient -Udomainname/fordodone //10.234.92.21/sharename
Password:
Domain=[DOMAINNAME] OS=[Windows 5.0] Server=[Windows 2000 LAN Manager]
smb: \> cd testdir
smb: \testdir\> get C
NT_STATUS_FILE_IS_A_DIRECTORY opening remote file \testdir\C
smb: \testdir\> prompt
smb: \testdir\> recurse
smb: \testdir\> mget C
getting file ...
```
