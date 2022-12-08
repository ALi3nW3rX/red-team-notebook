# LAPS



### Using CrackMapExec when LAPS installed on the domain

If LAPS is used inside the domain, is can be hard to use CrackMapExec to execute a command on every computer on the domain.

Therefore, a new core option has been added `--laps !` If you have compromised an accout that can read LAPS password you can use CrackMapExec like this

`crackmapexec winrm <ip> -u user-can-read-laps -p pass --laps`

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If the default administrator name is not administrator add the user after the option

`--laps name`
{% endhint %}
