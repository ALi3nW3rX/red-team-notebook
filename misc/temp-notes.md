# Temp - Notes

Exploiting GPP SYSVOL - cname password / Groups.xml

{% embed url="https://vk9-sec.com/exploiting-gpp-sysvol-groups-xml/" %}

{% embed url="https://byt3bl33d3r.github.io/practical-guide-to-ntlm-relaying-in-2017-aka-getting-a-foothold-in-under-5-minutes.html" %}

### Setting up network between Vbox and VMware

{% embed url="https://www.sysprobs.com/setup-network-virtualbox-vmware-virtual-machines" %}

### Check Recycle bin

you need the SID for the user that you want to check the recycle bin for.

```
cd 'C:\$Recycle.bin\S-1-5-21-1987495829-1628902820-919763334-1001'
```



Change password for user over rcpclient

{% code title="Output should be nothing." %}
```
rpcclient -U 'blackfield.local/support%#00^BlackKnight' 10.10.10.192 -c 'setuserinfo2 audit2020 23 "alien##123"'
```
{% endcode %}



### EVIL-WINRM for ATHNEA

```
👾]/home/ali3nw3rx $ sudo docker run --rm -ti --name evil-winrm  oscarakaelvis/evil-winrm -i 10.10.11.174 -u support -p 'Ironside47pleasure40Watchful'
```

runAS

{% embed url="https://github.com/antonioCoco/RunasCs" %}

{% embed url="https://steflan-security.com/windows-privilege-escalation-runas-stored-credentials/" %}

Chisel

{% embed url="https://github.com/jpillora/chisel/releases/tag/v1.7.7" %}

Juicy PotatoNG

{% embed url="https://github.com/antonioCoco/JuicyPotatoNG/releases/tag/v1.1" %}

Windows path traversal cheet sheat

{% embed url="https://gist.github.com/SleepyLctl/823c4d29f834a71ba995238e80eb15f9" %}
