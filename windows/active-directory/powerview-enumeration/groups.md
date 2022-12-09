# Groups

**List all groups of the domain**

```
Get-NetGroup
Get-NetGroup -GroupName *admin*
Get-NetGroup -Domain <domain>
```

**Get all the members of the group**

```
Get-NetGroupMember -Groupname "Domain Admins" -Recurse
Get-NetGroupMember -Groupname "Domain Admins" -Recurse | select MemberName
```

**Get the group membership of a user**

```
Get-NetGroup -Username <username>
```

**List all the local groups on a machine (needs admin privs on non dc machines)**

```
Get-NetlocalGroup -Computername <computername> -ListGroups
```

**Get Member of all the local groups on a machine (needs admin privs on non dc machines)**

```
Get-NetlocalGroup -Computername <computername> -Recurse
```
