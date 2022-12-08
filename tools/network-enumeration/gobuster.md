# GOBUSTER

#### Basic usage

```
gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt
```

#### DNS fuzzing

```
gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt
```
