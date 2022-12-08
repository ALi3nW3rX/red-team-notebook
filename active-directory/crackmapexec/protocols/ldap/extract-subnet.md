---
description: Extract subnet over an Active Directory environment
---

# Extract Subnet

```
$ poetry run crackmapexec ldap <ip> -u <user> -p <pass> -M get-network
$ poetry run crackmapexec ldap <ip> -u <user> -p <pass> -M get-network -o ONLY_HOSTS=true
$ poetry run crackmapexec ldap <ip> -u <user> -p <pass> -M get-network -o ALL=true
```

<figure><img src="../../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
