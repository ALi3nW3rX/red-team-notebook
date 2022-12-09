# Domain Enumeration

**Get Current Domain**

```
Get-NetDomain
```

**Get Object of another domain**

```
Get-NetDomain -Domain DomainName
```

**Get Domain SID for the current domain**

```
Get-DomainSID
```

**Get the domain password policy**

```
Get-DomainPolicy
(Get-DomainPolicy)."System Access"
net accounts
```

**Get Information of domain controller**

```
Get-NetDomainController
Get-NetDomainController | select-object Name
```
