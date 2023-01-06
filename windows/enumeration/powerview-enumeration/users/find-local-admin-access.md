# Find Local Admin Access

## Find Local Admin Access

```
Find-LocalAdminAccess -Verbose
```

## Find WMI Local Admin Access

```
. ./Find-WMILocalAdminAccess.ps1
Find-WMILocalAdminAccess
```

## Find PS Remoting with Local Admin Access

```
. ./Find-PSRemotingLocalAdminAccess.ps1
Find-PSRemotingLocalAdminAccess
```

## Find Local Admins on all machines in Domain

```
Invoke-EnumerateLocalAdmin -Verbose
```

## Find Interesting ACL's for a User

```
Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReferenceName -match "studentx"} 
```

## Find Interesting ACL's for a Group

```
Find-InterestingDomainAcl -ResolveGUIDs | ?{$_.IdentityReferenceName -match "RDPUsers"}
```

