# LinWinPwn

## Installation

Git clone the repository and make the script executable

```
git clone https://github.com/lefayjey/linWinPwn
cd linWinPwn; 
chmod +x linWinPwn.sh
chmod +x install.sh
```

Install requirements using the `install.sh` script

<pre><code><strong>sudo ./install.sh
</strong></code></pre>

linWinPwn is a bash script that automates a number of Active Directory Enumeration and Vulnerability checks. The script uses a number of tools and serves as wrapper of them. Tools include: impacket, bloodhound, crackmapexec, ldapdomaindump, lsassy, smbmap, kerbrute, adidnsdump, certipy, silenthound, and others.

linWinPwn is particularly useful when you have access to an Active Directory environment for a limited time only, and you wish to automate the enumeration process and collect evidence efficiently. In addition, linWinPwn can replace the use of enumeration tools on Windows in the aim of reducing the number of created artifacts (e.g., PowerShell commands, Windows Events, created files on disk), and bypassing certain Anti-Virus or EDRs. This can be achieved by performing remote dynamic port forwarding through the creation of an SSH tunnel from the Windows host (e.g., VDI machine or workstation or laptop) to a remote Linux machine (e.g., Pentest laptop or VPS), and running linWinPwn with proxychains.

## Usage

```powershell
#Basic Command
./linWinPwn.sh -t <Domain_Controller_IP> 

#Run With Username and Password
./linWinPwn.sh -t <Domain_Controller_IP> -u <username> -p <password>

#Run with above and domain name
./linWinPwn.sh -t <Domain_Controller_IP> -u <username> -p <password> -d <domain name>
```

## SSH Tunneling & Proxychains

On the Windows host, run using PowerShell:

```
ssh kali@<linux_machine> -R 1080 -NCqf
```

On the Linux machine, first update `/etc/proxychains4.conf` to include `socks5 127.0.0.1 1080`, then run:

```
proxychains ./linWinPwn.sh -t <Domain_Controller_IP>
```

{% embed url="https://github.com/lefayjey/linWinPwn" %}
