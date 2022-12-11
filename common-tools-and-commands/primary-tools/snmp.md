# SNMP

### <mark style="color:green;">SNMP</mark>

SNMP Community strings provide information and statistics about a router or device, helping us gain access to it. The manufacturer default community strings of public and private are often unchanged.&#x20;

In SNMP versions 1 and 2c, access is controlled using a plaintext community string, and if we know the name, we can gain access to it. Encryption and authentication were only added in SNMP version 3. Much information can be gained from SNMP.&#x20;

Examination of process parameters might reveal credentials passed on the command line, which might be possible to reuse for other externally accessible services given the prevalence of password reuse in enterprise environments. Routing information, services bound to additional interfaces, and the version of installed software can also be revealed.

#### <mark style="color:green;">SNMPWALK</mark>

```powershell
snmpwalk -v 2c -c public 10.10.10.10 1.3.6.1.2.1.1.5.0
##output = iso.3.6.1.2.1.1.5.0 = STRING: "gs-svcscan"

snmpwalk -v 2c -c private  10.129.42.253
```

#### <mark style="color:green;">OneSixtyOne</mark> - [https://github.com/trailofbits/onesixtyone](https://github.com/trailofbits/onesixtyone)

A tool such as onesixtyone can be used to brute force the community string names using a dictionary file of common community strings such as the dict.txt file included in the GitHub repo for the tool.

```
onesixtyone -c dict.txt 10.129.42.254
```

{% embed url="https://book.hacktricks.xyz/network-services-pentesting/pentesting-snmp/snmp-rce" %}
