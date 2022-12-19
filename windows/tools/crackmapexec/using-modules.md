# Using Modules



### Viewing available modules for a Protocol

Run `cme <protocol> -L` to view available modules for the specified protocol.

For example to view all modules for the SMB protocol:

```
#~ cme smb -L
[*] met_inject                Downloads the Meterpreter stager and injects it into memory
[*] get_keystrokes            Logs keys pressed, time and the active window
[*] empire_exec               Uses Empire's RESTful API to generate a launcher for the specified listener and executes it

-- SNIP --
```

### Using a module

Run `cme <protocol> <target(s)> -M <module name>`.

For example to run the SMB Mimikatz module:

```
#~ crackmapexec smb <target(s)> -u Administrator -p 'P@ssw0rd' -M mimikatz
```

### Viewing module options

Run `cme <protocol> -M <module name> --options` to view a modules supported options, e.g:

```
#~ cme smb -M mimikatz --options
```

### Using module options

Module options are specified with the `-o` flag. All options are specified in the form of KEY=value (msfvenom style)

Example:

```
#~ cme <protocol> <target(s)> -u Administrator -p 'P@ssw0rd' -M mimikatz -o COMMAND='privilege::debu
```
