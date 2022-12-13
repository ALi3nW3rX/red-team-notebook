# CrackMapExec

```
sudo apt install crackmapexec
```

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

## Target Formats

Every protocol supports targets by CIDR notation(s), IP address(s), IP range(s), hostname(s), a file containing a list of targets or combination of all of the latter:

```
crackmapexec <protocol> ms.evilcorp.org
```

```
crackmapexec <protocol> 192.168.1.0 192.168.0.2
```

```
crackmapexec <protocol> 192.168.1.0/24
```

```
crackmapexec <protocol> 192.168.1.0-28 10.0.0.1-67
```

```
crackmapexec <protocol> ~/targets.txt
```

## Using Credentials

Every protocol supports using credentials in one form or another. For details on using credentials with a specific protocol, see the appropriate wiki section.

Generally speaking, to use credentials, you can run the following commands:

```
crackmapexec <protocol> <target(s)> -u username -p password
```

{% hint style="info" %}
When using usernames or passwords that contain special symbols, wrap them in single quotes to make your shell interpret them as a string.
{% endhint %}

Example:

```
crackmapexec <protocol> <target(s)> -u username -p 'Admin!123@'
```

{% hint style="info" %}
Due to a [bug](https://bugs.python.org/issue9334) in Python's argument parsing library, credentials beginning with a dash (`-`) will throw an `expected at least one argument` error message. To get around this, specify the credentials by using the 'long' argument format (note the `=` sign):
{% endhint %}

`crackmapexec <protocol> <target(s)> -u='-username' -p='-Admin!123@'`

## Using a credential set from the database

By specifying a credential ID (or multiple credential IDs) with the `-id` flag CME will automatically pull that credential from the back-end database and use it to authenticate (saves a lot of typing):

```
crackmapexec <protocol> <target(s)> -id <cred ID(s)>
```

## Multi-domain environment

[https://github.com/byt3bl33d3r/CrackMapExec/issues/243](https://github.com/byt3bl33d3r/CrackMapExec/issues/243)

You can use CME with mulitple domain environment

```
crackmapexec <protocol> <target(s)> -p FILE -u password
```

Where **FILE** is a file with usernames in this format

```
DOMAIN1\user
DOMAIN2\user
```

## Brute Forcing & Password Spraying

All protocols support brute-forcing and password spraying. For details on brute-forcing/password spraying with a specific protocol, see the appropriate wiki section.

By specifying a file or multiple values CME will automatically brute-force logins for all targets using the specified protocol:

Examples:

```
crackmapexec <protocol> <target(s)> -u username1 -p password1 password2
```

```
crackmapexec <protocol> <target(s)> -u username1 username2 -p password1
```

```
crackmapexec <protocol> <target(s)> -u ~/file_containing_usernames -p ~/file_containing_passwords
```

```
crackmapexec <protocol> <target(s)> -u ~/file_containing_usernames -H ~/file_containing_ntlm_hashes
```

## Password Spraying without bruteforce

Can be usefull for protocols like WinRM and MSSQL. This option avoid the bruteforce when you use files (-u file -p file)

```
crackmapexec <protocol> <target(s)> -u ~/file_containing_usernames -H ~/file_containing_ntlm_hashes --no-bruteforce
```

```
crackmapexec <protocol> <target(s)> -u ~/file_containing_usernames -p ~/file_containing_passwords --no-bruteforce
```

```
user1 -> pass1
user2 -> pass2
```

{% hint style="info" %}
By default CME will exit after a successful login is found. Using the --continue-on-success flag will continue spraying even after a valid password is found. Usefull for spraying a single password against a large user list.
{% endhint %}

```
crackmapexec <protocol> <target(s)> -u ~/file_containing_usernames -H ~/file_containing_ntlm_hashes --no-bruteforce --continue-on-success
```
