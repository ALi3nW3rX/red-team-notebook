# Computers

**Get computer information**

```
Get-NetComputer
Get-NetComputer -FullData
Get-NetComputer -Computername <computername> -FullData
```

**Get computers with operating system**&#x20;

```
Get-NetComputer -OperatingSystem "*Server 2016*"
```

**Get list of all computer names and operating systems**

```
Get-NetComputer -fulldata | select samaccountname, operatingsystem, operatingsystemversion
```
