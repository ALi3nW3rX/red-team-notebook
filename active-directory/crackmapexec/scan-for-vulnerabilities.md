# Scan for Vulnerabilities



When you start your internal pentest, this is the first modules you should try:

### Zerologon

`crackmapexec smb <ip> -u '' -p '' -M zerologo`

### PetitPotam

`crackmapexec smb <ip> -u '' -p '' -M petitpotam`

### noPAC

`crackmapexec smb <ip> -u 'user' -p 'pass' -M nopac`

{% hint style="warning" %}
You need a credential for this one
{% endhint %}
