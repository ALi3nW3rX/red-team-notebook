# OU's

**Get OU's in a domain**

```
Get-NetOU -Fulldata
```

**Get machines that are part of an OU**

```
Get-NetOU StudentMachines | %{Get-NetComputer -ADSPath $_}
```
