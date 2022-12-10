# NMAP

### <mark style="color:green;">**NMAP**</mark>

```
nmap <ip>
```

<mark style="color:green;">**-sC**</mark>** ** - run nmap basic enumeration scripts

```
nmap -sC <ip>
```

<mark style="color:green;">**-sV**</mark>** ** - run nmap version scan

```
nmap -sV <ip>
```

<mark style="color:green;">**-p**</mark>  - specify a specific port to scan

```
nmap -p 80 <ip>
```

<mark style="color:green;">**-p-**</mark> - tells nmap to scan all 65,535 ports

```
nmap -p- <ip>
```

### <mark style="color:green;">Scripts</mark>

Scripts are tyically located in <mark style="color:green;">`/usr/share/nmap/scripts`</mark>. You can run any of the scripts in the dir with you nmap scans

```
nmap --script <script name> -p<port Number> <ip>

## Example

nmap -sV -Pn --script smb-enum-shares.nse -p445 10.10.10.10
```
