# ACL's

**Get the ACL's associated with the specified object**

```
Get-ObjectACL -SamAccountName <accountname> -ResolveGUIDS
```

**Get the ACL's associated with the specified prefix to be used for search**

```
Get-ObjectACL -ADSprefix ‘CN=Administrator,CN=Users’ -Verbose
```

**Get the ACL's associated with the specified path**

```
Get-PathAcl -Path \\<Domain controller>\sysvol
```

**Search for interesting ACL's**

```
Invoke-ACLScanner -ResolveGUIDs
Invoke-ACLScanner -ResolveGUIDs | select IdentityReference, ObjectDN, ActiveDirectoryRights | fl
```

**Search of interesting ACL's for the current user**

```
Invoke-ACLScanner | Where-Object {$_.IdentityReference –eq [System.Security.Principal.WindowsIdentity]::GetCurrent().Name}

```

**Check if student has replication rights**

```
Get-ObjectAcl -DistinguishedName "dc=dollarcorp,dc=moneycorp,dc=local" -ResolveGUIDs | ? {($_.IdentityReference -match "<username>") -and (($_.ObjectType -match 'replication') -or ($_.ActiveDirectoryRights -match 'GenericAll'))}
```
