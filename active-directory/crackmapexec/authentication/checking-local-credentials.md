# Checking Local Credentials

## User/Password/Hashes

Adding `--local-auth` to any of the authentication commands with attempt to logon locally.

```
#~ cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --local-auth
#~ cme smb 192.168.1.0/24 -u '' -p '' --local-auth
#~ cme smb 192.168.1.0/24 -u UserNAme -H 'LM:NT' --local-auth
#~ cme smb 192.168.1.0/24 -u UserNAme -H 'NTHASH' --local-auth
#~ cme smb 192.168.1.0/24 -u localguy -H '13b29964cc2480b4ef454c59562e675c' --local-auth
#~ cme smb 192.168.1.0/24 -u localguy -H 'aad3b435b51404eeaad3b435b51404ee:13b29964cc2480b4ef454c59562e675c' --local-auth
```

Results will display the hostname next to the user:password

```
	SMB         192.168.1.101    445    HOSTNAME          [+] HOSTNAME\Username:Password 
```
