# Authentication

## Testing credentials

You can use two methods to authenticate to the MSSQL: `windows` or `local` (default: `windows`). To use local auth, add the following flag `--local-auth`

### **Windows auth**

1. With SMB port open

```
#~ cme mssql 10.10.10.52 -u james -p 'J@m3s_P@ssW0rd!'
```

1. With SMB port close, add the flag `-d DOMAIN`

```
#~ cme mssql 10.10.10.52 -u james -p 'J@m3s_P@ssW0rd!' -d HTB
```

Expected Results:

```
MSSQL       10.10.10.52     1433   MANTIS           [+] HTB\james:J@m3s_P@ssW0rd! 
```

### **Local auth**

```
#~ cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --local-auth
```

Expected Results:

```
MSSQL       10.10.10.52     1433   None             [+] admin:m$$ql_S@_P@ssW0rd! (Pwn3d!)
```

### Specify Ports

```
#~ cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --port 1434
```
