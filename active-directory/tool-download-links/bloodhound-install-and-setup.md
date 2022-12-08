# BloodHound Install & Setup

Download and Install Bloodhound

{% embed url="https://github.com/BloodHoundAD/BloodHound" %}

{% embed url="https://github.com/neo4j/neo4j" %}

```
. ./sharphound.ps1
Invoke-Bloodhound -CollectionMethod all -Verbose
Invoke-Bloodhound -CollectionMethod LoggedOn -Verbose

#Copy neo4j-community-3.5.1 to C:\

#Open cmd
cd C:\neo4j\neo4j-community-3.5.1-windows\bin
neo4j.bat install-service
neo4j.bat start

#Browse to BloodHound-win32-x64
Run BloodHound.exe

#Change credentials and login
```
