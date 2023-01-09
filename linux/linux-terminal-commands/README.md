# Linux Terminal Commands

## Linux Terminal Commands

## Find Programs Accessible to User:

```powershell
find / -perm -4000 2>/dev/null 

find / -perm -u=s -type f 2>/dev/null

find / -name user.txt 2>/dev/null

find / -perm -u=s -type f 2>/dev/null | xarg ls -la
```

## Basic Enumeration Commands

```powershell
uname -a # kernel details
/proc/version # process information
/etc/issue # info on changes or customizations
ps # running process
ps aux
ps -A
ps axjf
env # environment variables
sudo -l # sees what sudo commands 'we' can run
id # current user privileges
/etc/passwd # discover users
/etc/passwd | cut -d ":" -f 
/etc/passwd | grep home
history # shows user history of commands
ifconfig # net info
iproute # net routes

find. -name flag.txt
find /home -name flag.txt
find / -type d -name config
find / -type f -perm 0777
find / -perm a=x
find /home -user frank
find / -mtime
find / -atime
find / -cmin
find / -amin
find / -size +/- 50m
find / -writable -type d 2>/dev/null
find / -writable -type f 2>/dev/null
find / -perm -222 -type d 2>/dev/null
find / -perm -o w -type d 2>/dev/null
find / -perm -o x -type d 2>/dev/null
find / -name python*

getcap -r / 2>/dev/null # get capapbilities
```

## Enumeration

```powershell
ls /etc/*-release # looks for version numbers

cat /etc/os-release # cat out the file with the version numbers

hostname # return hostname of target

cat /etc/passwd # read passwd file for possible users

cat /etc/group # read groups for possible users

sudo cat /etc/shadow # read out shadow file for password hashes

ls -lh /var/mail # checks mail directories

ls /usr/bin/ & /sbin # for applications 

rpm -qa # list installed packages on RPM linux distro

dpkg -l # list installed packages on Debian linux distro

who # shows logged in users

whoami # shows what user you are logged in as

w # shows who is logged in and what they are doing

id # gives you your current UID and Group

last # displays login and logout info for users

sudo -l # what commands we can run sudo as
```

## Networking

```powershell
ip a s # shows current ip

cat /etc/resolv.conf -> shows the DNS servers

netstat # shows info about network connections
	-a # show both listening and non-listening sockets
	-l # show only listening sockets
	-n # show numeric output instead of resolving the IP address and port number
	-t # TCP
	-u # UDP
	-x # UNIX
	-p # show the PID and name of the program to which the socket belongs

sudo netstat -atupn # show all TCP / UDP listening and established conn with ports

sudo lsof -i # List of open files

sudo lsof - :port number # Checks for open files on a specific port
```

## Running Services

```powershell
ps # snapshot of running process on the machine
	-e # all processes
	-f # full-format listing
	-j # jobs format
	-l # long format
	-u # user-orented format
	
ps aux # displays all processes	
ps axjf # displays all processes in a "tree" format
```

```powershell
sudo awk 'BEGIN {system("/bin/sh")}'
sudo find /etc -exec sh -i \;
sudo tcpdump -n -i lo -G1 -w /dev/null -z ./runme.sh
sudo tar c a.tar -I ./runme.sh a
ftp>!/bin/sh
less>! <shell_comand>
```
