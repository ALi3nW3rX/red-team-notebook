---
description: >-
  This article will cover all of the basics of attacking Kerberos the windows
  ticket-granting service; we'll cover the following:
---

# Attacking Kerberos

* Initial enumeration using tools like Kerbrute and Rubeus&#x20;
* Kerberoasting AS-REP Roasting with Rubeus and Impacket&#x20;
* Golden/Silver Ticket Attacks&#x20;
* Pass the Ticket&#x20;
* Skeleton key attacks using mimikatz

This room will be related to very real-world applications and will most likely not help with any CTFs however it will give you great starting knowledge of how to escalate your privileges to a domain admin by attacking Kerberos and allow you to take over and control a network.

### What is Kerberos?&#x20;

Kerberos is the default authentication service for Microsoft Windows domains. It is intended to be more "secure" than NTLM by using third party ticket authorization as well as stronger encryption. Even though NTLM has a lot more attack vectors to choose from Kerberos still has a handful of underlying vulnerabilities just like NTLM that we can use to our advantage.

<details>

<summary><mark style="color:green;"><strong>Common Terminology</strong></mark></summary>

* <mark style="color:green;">**Ticket Granting Ticket (TGT)**</mark> - A ticket-granting ticket is an authentication ticket used to request service tickets from the TGS for specific resources from the domain.

<!---->

* <mark style="color:green;">**Key Distribution Center (KDC)**</mark> - The Key Distribution Center is a service for issuing TGTs and service tickets that consist of the Authentication Service and the Ticket Granting Service.

<!---->

* <mark style="color:green;">**Authentication Service (AS)**</mark> - The Authentication Service issues TGTs to be used by the TGS in the domain to request access to other machines and service tickets.

<!---->

* <mark style="color:green;">**Ticket Granting Service (TGS)**</mark> - The Ticket Granting Service takes the TGT and returns a ticket to a machine on the domain.

<!---->

* <mark style="color:green;">**Service Principal Name (SPN)**</mark> - A Service Principal Name is an identifier given to a service instance to associate a service instance with a domain service account. Windows requires that services have a domain service account which is why a service needs an SPN set.

<!---->

* <mark style="color:green;">**KDC Long Term Secret Key (KDC LT Key)**</mark> - The KDC key is based on the KRBTGT service account. It is used to encrypt the TGT and sign the PAC.

<!---->

* <mark style="color:green;">**Client Long Term Secret Key (Client LT Key)**</mark> - The client key is based on the computer or service account. It is used to check the encrypted timestamp and encrypt the session key.

<!---->

* <mark style="color:green;">**Service Long Term Secret Key (Service LT Key)**</mark> - The service key is based on the service account. It is used to encrypt the service portion of the service ticket and sign the PAC.

<!---->

* <mark style="color:green;">**Session Key**</mark> - Issued by the KDC when a TGT is issued. The user will provide the session key to the KDC along with the TGT when requesting a service ticket.

<!---->

* <mark style="color:green;">**Privilege Attribute Certificate (PAC)**</mark> - The PAC holds all of the user's relevant information, it is sent along with the TGT to the KDC to be signed by the Target LT Key and the KDC LT Key in order to validate the user.

</details>

### AS-REQ w/ Pre-Authentication In Detail

The AS-REQ step in Kerberos authentication starts when a user requests a TGT from the KDC. In order to validate the user and create a TGT for the user, the KDC must follow these exact steps. The first step is for the user to encrypt a timestamp NT hash and send it to the AS. The KDC attempts to decrypt the timestamp using the NT hash from the user, if successful the KDC will issue a TGT as well as a session key for the user.

### Ticket Granting Ticket Contents

In order to understand how the service tickets get created and validated, we need to start with where the tickets come from; the TGT is provided by the user to the KDC, in return, the KDC validates the TGT and returns a service ticket.

### Service Ticket Contents

To understand how Kerberos authentication works you first need to understand what these tickets contain and how they're validated. A service ticket contains two portions: the service provided portion and the user-provided portion. I'll break it down into what each portion contains.

* <mark style="color:green;">**Service Portion:**</mark> User Details, Session Key, Encrypts the ticket with the service account NTLM hash.
* <mark style="color:green;">**User Portion:**</mark> Validity Timestamp, Session Key, Encrypts with the TGT session key.

<details>

<summary><mark style="color:green;"><strong>Kerberos Authentication Overview</strong></mark></summary>

* <mark style="color:green;">**AS-REQ**</mark> - 1<mark style="color:green;">**.**</mark> The client requests an Authentication Ticket or Ticket Granting Ticket (TGT)

<!---->

* <mark style="color:green;">**AS-REP**</mark> - 2. The Key Distribution Center verifies the client and sends back an encrypted TGT

<!---->

* <mark style="color:green;">**TGS-REQ**</mark> - 3. The client sends the encrypted TGT to the Ticket Granting Server (TGS) with the Service Principal Name (SPN) of the service the client wants to access

<!---->

* <mark style="color:green;">**TGS-REP**</mark> - 4. The Key Distribution Center (KDC) verifies the TGT of the user and that the user has access to the service, then sends a valid session key for the service to the client

<!---->

* <mark style="color:green;">**AP-REQ**</mark> - 5. The client requests the service and sends the valid session key to prove the user has access

<!---->

* <mark style="color:green;">**AP-REP**</mark> - 6. The service grants access

</details>

### Kerberos Tickets Overview

The main ticket that you will see is a <mark style="color:green;">**ticket-granting ticket**</mark> these can come in various forms such as a .kirbi for Rubeus .cache for Impacket. The main ticket that you will see is a .kirbi ticket. A ticket is typically base64 encoded and can be used for various attacks. The ticket-granting ticket is only used with the KDC in order to get service tickets.&#x20;

Once you give the TGT the server then gets the User details, session key, and then encrypts the ticket with the service account NTLM hash. Your TGT then gives the encrypted timestamp, session key, and the encrypted TGT. The KDC will then authenticate the TGT and give back a service ticket for the requested service. A normal TGT will only work with that given service account that is connected to it however a KRBTGT allows you to get any service ticket that you want allowing you to access anything on the domain that you want.

### Attack Privilege Requirements

* <mark style="color:green;">**Kerbrute Enumeration**</mark> - No domain access required
* <mark style="color:green;">**Pass the Ticket**</mark> - Access as a user to the domain required
* <mark style="color:green;">**Kerberoasting**</mark> - Access as any user required
* <mark style="color:green;">**AS-REP Roasting**</mark> - Access as any user required
* <mark style="color:green;">**Golden Ticket**</mark> - Full domain compromise (domain admin) required
* <mark style="color:green;">**Silver Ticket**</mark> - Service hash required
* <mark style="color:green;">**Skeleton Key**</mark> - Full domain compromise (domain admin) required

<details>

<summary><mark style="color:green;">Task 1 Questions and Answers</mark></summary>

1. What does TGT stand for?                                     <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**Ticket Granting Ticket**</mark> &#x20;
2. What does SPN stand for?                                    <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**Service Principal Name**</mark> &#x20;
3. What does PAC stand for?                                    <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**Privilege Attribute Certificate**</mark> &#x20;
4. What 2 services make up the KDC?                     <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**as, tgs**</mark> &#x20;
5. Deploy machine.

</details>

Task 2 we are going to use a tool called Kerbrute to enumerate users on our target machine. You can download and install the pre-compiled binaries directly off of github [ https://github.com/ropnop/kerbrute/releases](https://github.com/ropnop/kerbrute/releases)

Or you can run this command to install with go.&#x20;

<mark style="color:green;">**`go install github.com/ropnop/kerbrute@latest`**</mark>

Step 1. Download or install Kerbrute

Step 2. Download the User.txt file with possible usernames.

Step 3. User Kerbrute to enumerate Kerberos for possible active usernames we can use.



The command that THM wants us to run is:

<mark style="color:green;">`./kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt`</mark>  or

<mark style="color:green;">`kerbrute userenum --dc CONTROLLER.local -d CONTROLLER.local User.txt`</mark>

depending on how you installed Kerbrute. However if your like me and don't read directions you might get something that looks like this below.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

To fix this we simply have to edit our /etc/hosts file with our IP and DNS information.

<mark style="color:green;">`sudo nano /etc/hosts`</mark>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Once you save and exit we can run the above command again to start enumerating usernames.

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Great! Now we have a list of possible usernames that we can work with.

<details>

<summary><mark style="color:green;"><strong>Task 2 Questions and Answers</strong></mark></summary>

1. How many total users do we enumerate?                                      <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**10**</mark> &#x20;
2. What is the SQL service account name?                                       <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**sqlservice**</mark> &#x20;
3. What is the second "machine" account name?                             <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**machine2**</mark> &#x20;
4. What is the thrid "user" account name?                                         <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**user3**</mark> &#x20;

</details>

For Task 3 we need to RDP into the machine. I preferer Remmina but you can use what ever you feel comfortable with.&#x20;

![](<../../.gitbook/assets/image (13).png>) ![](<../../.gitbook/assets/image (26).png>) ![](<../../.gitbook/assets/image (28).png>)![](<../../.gitbook/assets/image (61).png>)

If done correctly you should be brought to a screen that looks like this.&#x20;

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

To make it full screen go ahead and click on this button on the left menu panel

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

### Harvesting Tickets w/ Rubeus

We are going to open a command prompt on our windows machine and navigate over to the /Downloads dir. Then run the following command

<mark style="color:green;">`C:\Users\Administrator\Downloads>Rubeus.exe harvest /interval:30`</mark>

This is going to tell Rubeus to harvest tickets every 30 seconds

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

### Brute-Forcing / Password-Spraying w/ Rubeus

Rubeus can both brute force passwords as well as password spray user accounts. When brute-forcing passwords you use a single user account and a wordlist of passwords to see which password works for that given user account. In password spraying, you give a single password such as Password1 and "spray" against all found user accounts in the domain to find which one may have that password.

This attack will take a given Kerberos-based password and spray it against all found users and give a .kirbi ticket. This ticket is a TGT that can be used in order to get service tickets from the KDC as well as to be used in attacks like the pass the ticket attack.

Before password spraying with Rubeus, you need to add the domain controller domain name to the windows host file. You can add the IP and domain name to the hosts file from the machine by using the echo command:

<mark style="color:green;">**`echo 10.10.142.7 CONTROLLER.local >> C:\Windows\System32\drivers\etc\hosts`**</mark>

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

Now we can run a brute force attack:

<mark style="color:green;">**`Rubeus.exe brute /password:Password1 /noticket`**</mark>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<details>

<summary><mark style="color:green;"><strong>Task 3 Questions and Answers</strong></mark></summary>

1. Which domain admin do we get a ticket for when harvesting tickets? We can run <mark style="color:green;">`klist`</mark> to see our tickets our machine.    <mark style="background-color:green;">**Administrator**</mark> &#x20;

<img src="../../.gitbook/assets/image (53).png" alt="" data-size="original">

1. Which domain controller do we get a ticket for when harvesting tickets? We see that when we ran the harvester our 'user' was    <mark style="background-color:green;">**CONTOLLER-1$**</mark> &#x20;

![](<../../.gitbook/assets/image (32).png>)

</details>

### Kerberoasting w/ Rubeus

Navigate to the downloads folder in a terminal and run the following command:

<mark style="color:green;">**`C:\Users\Administrator\Downloads>Rubeus.exe kerberoast`**</mark>

We get 2 hashes, one for SQLservice and another from HTTPservice

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
If for some reason Rubeus.exe disappears from your windows machine, you can host it on your kali vm and re download it. Don't run it just save it back to the downloads folder and run it from the command prompt.
{% endhint %}

Now, we can take that giant hash and crack it with Hashcat or John to get a clear text password. Note, when you copy these hashes they have to be in a single line (at least for hashcat) for them to crack properly.



<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Kerberoasting w/ Impacket

With Impacket we don't have to RDP into a machine or even be connected. We can do this attack remotely. To run this attack type the following command in your attack machine terminal:

<mark style="color:green;">**sudo python3 GetUserSPNs.py controller.local/Machine1:Password1 -dc-ip 10.10.142.7 -request**</mark>

Cool! We get the same hashes, and we did it remotely!&#x20;

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

We can now copy and paste those hashes into a text file and run it against hashcat to get the passwords. However if we run it like this it won't give us the correct answers for the questions. Also when we use Rubeus.exe we krbtgs hashes back and when we run impacket we get asrep hashes back.&#x20;

With Impacket:

_<mark style="color:green;">**$krb5asrep**</mark>_~~<mark style="color:green;">**$23$User3@CONTROLLER.LOCAL:962403b3883b90e97b7da880601**</mark>~~

With Rubeus:

_<mark style="color:green;">**$krb5tgs**</mark>_~~<mark style="color:green;">**$23$**</mark>_<mark style="color:green;">**HTTPService$CONTROLLER.local$CONTROLLER-1/HTTPService.CON**</mark>_~~

Hashcat will crack both of these but we need to make sure we are using the right mode in hashcat to do so. Also the answers on Tryhackme are looking for the service tickets that we get from Rubeus.

{% embed url="https://hashcat.net/wiki/doku.php?id=example_hashes" %}

<details>

<summary><mark style="color:green;"><strong>Task 4 Questions and Answers</strong></mark> </summary>

1. What is the HTTPService Password?                <mark style="color:green;background-color:green;"></mark>  <mark style="color:green;"><mark style="background-color:green;">**S**<mark style="background-color:green;"></mark><mark style="background-color:green;">**ummer2020**</mark>         &#x20;
2. What is the SQLService Password?                  <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**MYPassword123#**</mark> &#x20;

</details>

### AS-REP Roasting Overview

Very similar to Kerberoasting, AS-REP Roasting dumps the krbasrep5 hashes of user accounts that have Kerberos pre-authentication disabled. Unlike Kerberoasting these users do not have to be service accounts the only requirement to be able to AS-REP roast a user is the user must have pre-authentication disabled.

We'll continue using Rubeus same as we have with kerberoasting and harvesting since Rubeus has a very simple and easy to understand command to AS-REP roast and attack users with Kerberos pre-authentication disabled. After dumping the hash from Rubeus we'll use hashcat in order to crack the krbasrep5 hash.

There are other tools out as well for AS-REP Roasting such as kekeo and Impacket's GetNPUsers.py. Rubeus is easier to use because it automatically finds AS-REP Roastable users whereas with GetNPUsers you have to enumerate the users beforehand and know which users may be AS-REP Roastable.

During pre-authentication, the users hash will be used to encrypt a timestamp that the domain controller will attempt to decrypt to validate that the right hash is being used and is not replaying a previous request. After validating the timestamp the KDC will then issue a TGT for the user. If pre-authentication is disabled you can request any authentication data for any user and the KDC will return an encrypted TGT that can be cracked offline because the KDC skips the step of validating that the user is really who they say that they are.

In our windows machine we are going to run the command:

<mark style="color:green;">**`C:\Users\Administrator\Downloads>Rubeus.exe asreproast`**</mark>

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

If you notice we get the <mark style="color:green;">`krb5asrep`</mark> hashes that we got before with impacket in the previous steps. When you get these hashes from Rubeus we need to add a <mark style="color:green;">**`23$`**</mark> after <mark style="color:green;">**`$krb5asrep$`**</mark> or hashcat won't be able to crack it. Impacket does this automatically for us.

Once we have those hashes in a text file we can use the following command to crack them:

<mark style="color:green;">**`hashcat -a 0 -m 18200 hashes2.txt Pass.txt`**</mark>

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

<details>

<summary><mark style="color:green;"><strong>Task 5 Questions and Answers</strong></mark></summary>

1. What hash type does AS-REP Roasting use?               <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**Kerberos 5, etype 23, AS-REP**</mark> &#x20;
2. Which User is vulnerable to AS-REP Roasting?           <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**User3**</mark>&#x20;
3. What is the User's Password?                                       <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**Password3**</mark> &#x20;
4. Which Admin is vulnerable to AS-REP Roasting?         <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**admin2**</mark> &#x20;
5. What is the Admin's Password?                                     <mark style="background-color:green;">**P@\$$w0rd2**</mark> &#x20;

</details>

### Pass the Ticket Overview

Pass the ticket works by dumping the TGT from the LSASS memory of the machine. The Local Security Authority Subsystem Service (LSASS) is a memory process that stores credentials on an active directory server and can store Kerberos ticket along with other credential types to act as the gatekeeper and accept or reject the credentials provided.&#x20;

You can dump the Kerberos Tickets from the LSASS memory just like you can dump hashes. When you dump the tickets with mimikatz it will give us a .kirbi ticket which can be used to gain domain admin if a domain admin ticket is in the LSASS memory. This attack is great for privilege escalation and lateral movement if there are unsecured domain service account tickets laying around.&#x20;

The attack allows you to escalate to domain admin if you dump a domain admin's ticket and then impersonate that ticket using mimikatz PTT attack allowing you to act as that domain admin. You can think of a pass the ticket attack like reusing an existing ticket were not creating or destroying any tickets here were simply reusing an existing ticket from another user on the domain and impersonating that ticket.

Unfortunately, on this machine Mimikatz was not working properly, I'm assuming because this is a PoC module. However you can do the same attack with Rubeus. You could simply copy and paste the base64 encoded ticket we got from harvesting and inject it as well.

<mark style="color:green;">**`C:\Users\Administrator\Downloads>Rubeus.exe ptt /ticket:doIFjDCCBYigAwI......`**</mark>

Then check to make sure the ticket was injected correctly by running: <mark style="color:green;">**`klist`**</mark>

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

### KRBTGT Overview

In order to fully understand how these attacks work you need to understand what the difference between a KRBTGT and a TGT is. A KRBTGT is the service account for the KDC this is the Key Distribution Center that issues all of the tickets to the clients.

If you impersonate this account and create a golden ticket form the KRBTGT you give yourself the ability to create a service ticket for anything you want. A TGT is a ticket to a service account issued by the KDC and can only access that service the TGT is from like the SQLService ticket.

### Golden/Silver Ticket Attack Overview

A golden ticket attack works by dumping the ticket-granting ticket of any user on the domain this would preferably be a domain admin however for a golden ticket you would dump the krbtgt ticket and for a silver ticket, you would dump any service or domain admin ticket.

This will provide you with the service/domain admin account's SID or security identifier that is a unique identifier for each user account, as well as the NTLM hash. You then use these details inside of a mimikatz golden ticket attack in order to create a TGT that impersonates the given service account information.

### Preparing Mimikatz

Navigate to /Downloads (in an elevated shell) and run <mark style="color:green;">**`Mimikatz.exe`**</mark>. Next we will run <mark style="color:green;">**`privilege::debug`**</mark> to allow us to run commands. Now, we can run the following command to dump the hashes and SID's that we need to create a Golden ticket.

<mark style="color:green;">**`mimikatz# lsadump::lsa /inject /name:krbtgt`**</mark>

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

### Create a Golden

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Create a Silver Ticket

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

To create the silver ticket the syntax is almost identical. We need to change out the NTLM hash with a service account NTLM hash, change out the SID to the service account and change the ID to 1103.&#x20;

<mark style="color:green;">**`mimikatz# misc::cmd`**</mark>

Will create a new process with your ticket so you can access different services or machines on the network.

Access machines that you want, what you can access will depend on the privileges of the user that you decided to take the ticket from however if you took the ticket from krbtgt you have access to the ENTIRE network hence the name golden ticket; however, silver tickets only have access to those that the user has access to if it is a domain admin it can almost access the entire network however it is slightly less elevated from a golden ticket.

<details>

<summary>Task 7 Questions and Answers</summary>

1. What is the SQLService NTLM hash?           <mark style="background-color:green;"></mark>  <mark style="background-color:green;"></mark><mark style="background-color:green;">**cd40c9ed96265531b21fc5b1dafcfb0a**</mark> &#x20;
2. What is the Administrator NTLM hash?       <mark style="background-color:green;"></mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**2777b7fec870e04dda00cd7260f7bee6**</mark> &#x20;

</details>

{% hint style="info" %}
To get the answers above simply run the command:\
mimikatz# lsadump::lsa /inject /name:\<PLACE NAME HERE>
{% endhint %}

### Skeleton Key Attack

This is an easy attack, however be careful because you can break the DC when you run this.

<mark style="color:green;">**`mimikatz# misc::skeleton`**</mark>

The default credentials will be: <mark style="color:green;">**`"mimikatz"`**</mark>

example: <mark style="color:green;">**`net use c:\DOMAIN-CONTROLLER\admin$ /user:Administrator mimikatz`**</mark> - The share will now be accessible without the need for the Administrators password

example: <mark style="color:green;">**`dir \Desktop-1\c$ /user:Machine1 mimikatz`**</mark> - access the directory of Desktop-1 without ever knowing what users have access to Desktop-1

The skeleton key will not persist by itself because it runs in the memory, it can be scripted or persisted using other tools and techniques.
