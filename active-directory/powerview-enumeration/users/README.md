# Users

**Get information of users in the domain**

```
Get-NetUser
Get-NetUser -Username <username>
```

**Get list of all users**

```
Get-NetUser | select samaccountname
```

**Get list of usernames, last logon and password last set**

```
Get-NetUser | select samaccountname, lastlogon, pwdlastset
Get-NetUser | select samaccountname, lastlogon, pwdlastset | Sort-Object -Property lastlogon
```

**Get list of usernames and their groups**

```
Get-NetUser | select samaccountname, memberof
```

**Get list of all properties for users in the current domain**

```
get-userproperty -Properties pwdlastset
```

**Get description field from the user**

```
Find-UserField -SearchField Description -SearchTerm "built"
Get-netuser | Select-Object samaccountname,description
```

**Get actively logged users on a computer (needs local admin privs)**

```
Get-NetLoggedon -Computername <computername>
```

**Get locally logged users on a computer (needs remote registry rights on the target)**

```
Get-LoggedonLocal -Computername <computername>
```

**Get the last logged users on a computer (needs admin rights and remote registary on the target)**

```
Get-LastLoggedOn -ComputerName <computername>
```



****



****



****
