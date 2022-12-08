# Using The Database



CME automatically stores all used/dumped credentials (along with other information) in it's database which is setup on first run.

As of CME v4 each protocol has it's own database which makes things much more sane and allows for some awesome possibilities. Additionally, v4 introduces workspaces (similar to Metasploit).

For details and usage of a specific protocol's database see the appropriate wiki section.

All workspaces and their relative databases are stored in `~/.cme/workspaces`

## Interacting with the Database

CME ships with a secondary command line script `cmedb` which abstracts interacting with the back-end database. Typing the command `cmedb` will drop you into a command shell:

```
#~ cmedb
cmedb (default) >
```

## Workspaces

The default workspace name is called 'default' (as represented within the prompt), once a workspace is selected everything that you do in CME will be stored in that workspace.

To create a workspace:

```
cmedb (default) > workspace create test
[*] Creating workspace 'test'
[*] Initializing HTTP protocol database
[*] Initializing SMB protocol database
[*] Initializing MSSQL protocol database
cmedb (test) >
```

To switch workspace:

```
cmedb (test) > workspace default
cmedb (default) >
```

## Accessing a Protocol's Database

To access a protocol's database simply run `proto <protocol>`, for example:

```
cmedb (test) > proto smb
cmedb (test)(smb) >
```

As you can see by the prompt, we are now in the workspace called 'test' and using the SMB protocol's database. Every protocol database has its own set of commands, you can run `help` to view available commands.

Please refer to the appropriate wiki section for details and usage of a specific protocol's database.

To switch protocol database:

```
cmedb (test)(smb) > back
cmedb (test) > proto http
cmedb (test)(http) >
```

## &#x20;:new: Export the database

You can export the datadase in a CSV format

```
cmedb (test)(smb) > export shares detailed file.csv
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
