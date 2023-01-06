# LLMNR/NBT-NS Poisoning - from Linux

[Link-Local Multicast Name Resolution](https://datatracker.ietf.org/doc/html/rfc4795) (LLMNR) and [NetBIOS Name Service](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc940063\(v=technet.10\)?redirectedfrom=MSDN) (NBT-NS) are Microsoft Windows components that serve as alternate methods of host identification that can be used when DNS fails.&#x20;

If a machine attempts to resolve a host but DNS resolution fails, typically, the machine will try to ask all other machines on the local network for the correct host address via LLMNR. LLMNR is based upon the Domain Name System (DNS) format and allows hosts on the same local link to perform name resolution for other hosts. It uses port `5355` over UDP natively.&#x20;

If LLMNR fails, the NBT-NS will be used. NBT-NS identifies systems on a local network by their NetBIOS name. NBT-NS utilizes port `137` over UDP.

The kicker here is that when LLMNR/NBT-NS are used for name resolution, ANY host on the network can reply.

This is where we come in with `Responder` to poison these requests. With network access, we can spoof an authoritative name resolution source ( in this case, a host that's supposed to belong in the network segment ) in the broadcast domain by responding to LLMNR and NBT-NS traffic as if they have an answer for the requesting host.&#x20;

This poisoning effort is done to get the victims to communicate with our system by pretending that our rogue system knows the location of the requested host. If the requested host requires name resolution or authentication actions, we can capture the NetNTLM hash and subject it to an offline brute force attack in an attempt to retrieve the cleartext password.&#x20;

The captured authentication request can also be relayed to access another host or used against a different protocol (such as LDAP) on the same host. LLMNR/NBNS spoofing combined with a lack of SMB signing can often lead to administrative access on hosts within a domain. SMB Relay attacks will be covered in a later module about Lateral Movement.

We are performing these actions to collect authentication information sent over the network in the form of NTLMv1 and NTLMv2 password hashes. As discussed in the [Introduction to Active Directory](https://academy.hackthebox.com/course/preview/introduction-to-active-directory) module, NTLMv1 and NTLMv2 are authentication protocols that utilize the LM or NT hash.&#x20;

We will then take the hash and attempt to crack them offline using tools such as [Hashcat](https://hashcat.net/hashcat/) or [John](https://www.openwall.com/john/) with the goal of obtaining the account's cleartext password to be used to gain an initial foothold or expand our access within the domain if we capture a password hash for an account with more privileges than an account that we currently possess.

| **Tool**                                              | **Description**                                                                                     |
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [Responder](https://github.com/lgandx/Responder)      | Responder is a purpose-built tool to poison LLMNR, NBT-NS, and MDNS, with many different functions. |
| [Inveigh](https://github.com/Kevin-Robertson/Inveigh) | Inveigh is a cross-platform MITM platform that can be used for spoofing and poisoning attacks.      |
| [Metasploit](https://www.metasploit.com/)             | Metasploit has several built-in scanners and spoofing modules made to deal with poisoning attacks.  |

```
lab_adm::INLANEFREIGHT:df5abaeb64185202:5E717FFC269C12E09A6DA6FD55C4F624:010100000000000041ADEFF9B60ED90160BE85F105B613580000000002000800580056004A00380001001E00570049004E002D00390050004300520052003700480057004E003700450004001400580056004A0038002E004C004F00430041004C0003003400570049004E002D00390050004300520052003700480057004E00370045002E00580056004A0038002E004C004F00430041004C0005001400580056004A0038002E004C004F00430041004C000800300030000000000000000000000000300000743F935961283F64BAA5A866993BF125129AABD0076CCB8906D5355156650D9A0A0010000000000000000000000000000000000009003A004D005300530051004C005300760063002F00610063006100640065006D0079002D00650061002D0077006500620030003A0031003400330033000000000000000000
svc_qualys::INLANEFREIGHT:d51ff848108e6034:87E68DDFF8B3B912696C36B05025C9C8:0101000000000000802B0FC3890ED9013A82941F645A54FA00000000020008004A0049004300360001001E00570049004E002D005A004C004A004F0039003500450057004A004300530004003400570049004E002D005A004C004A004F0039003500450057004A00430053002E004A004900430036002E004C004F00430041004C00030014004A004900430036002E004C004F00430041004C00050014004A004900430036002E004C004F00430041004C0007000800802B0FC3890ED90106000400020000000800300030000000000000000000000000300000743F935961283F64BAA5A866993BF125129AABD0076CCB8906D5355156650D9A0A001000000000000000000000000000000000000900220063006900660073002F003100370032002E00310036002E0035002E003200320035000000000000000000
wley::INLANEFREIGHT:fb6c1d8d445b28c4:049BABBDC98FD13C9E4C5FC44C7C6823:0101000000000000802B0FC3890ED9018D5A653913AD787B00000000020008004A0049004300360001001E00570049004E002D005A004C004A004F0039003500450057004A004300530004003400570049004E002D005A004C004A004F0039003500450057004A00430053002E004A004900430036002E004C004F00430041004C00030014004A004900430036002E004C004F00430041004C00050014004A004900430036002E004C004F00430041004C0007000800802B0FC3890ED90106000400020000000800300030000000000000000000000000300000743F935961283F64BAA5A866993BF125129AABD0076CCB8906D5355156650D9A0A001000000000000000000000000000000000000900220063006900660073002F003100370032002E00310036002E0035002E003200320035000000000000000000
clusteragent::INLANEFREIGHT:b8909404cc77e7e4:03CDC9DEB0E5B14CB4C736E5B95AB65C:0101000000000000802B0FC3890ED901ED17A59B04FE02D200000000020008004A0049004300360001001E00570049004E002D005A004C004A004F0039003500450057004A004300530004003400570049004E002D005A004C004A004F0039003500450057004A00430053002E004A004900430036002E004C004F00430041004C00030014004A004900430036002E004C004F00430041004C00050014004A004900430036002E004C004F00430041004C0007000800802B0FC3890ED90106000400020000000800300030000000000000000000000000300000743F935961283F64BAA5A866993BF125129AABD0076CCB8906D5355156650D9A0A001000000000000000000000000000000000000900220063006900660073002F003100370032002E00310036002E0035002E003200320035000000000000000000

```

wley = transporter@4\
svc\_qualys = security#1
