# SSH

{% embed url="https://github.com/dennyzhang/cheatsheet-ssh-A4/blob/master/README.org" %}

Generate new ssh keys

```
ssh-keygen -t rsa
```

The SSH authorized\_keys file is a file that contains a list of public keys that are authorized to log in to the server. This file is used to prevent unauthorized users from connecting to the SSH server.

SSH daemon on the server side checks whether the SSH key is correct or not by calculating the SSH key fingerprint.  If the SSH key is correct, it allows the user to log in without asking username or password.

The primary purpose of this guide is to illustrate the use of the \~/.ssh/authorized\_keys file. After reading this article, we will know how ssh authentication works, what the ssh authorized\_keys file is, and how to protect our account using ssh authorized\_keys. SSH daemon on the SSH server side verifies the SSH key by reading this file.

#### <mark style="color:green;">Understanding SSH authorized\_keys</mark>

The ssh protocol has 2 sides: the client and the server. The SSH key-based authentication uses ssh keys to verify that the user is authorized. If the ssh key is correct, it allows user to login without asking username or password.

* SSH keys do not provide any kind of network level access like telnet does.
* SSH keys are used for authentication and encryption.
* SSH keys are used to ssh into remote machine, not for remote desktop access.

#### <mark style="color:green;">Format of SSH authorized\_keys file</mark>

The authorized\_keys file contains SSH public key. SSH daemon on server side checks that SSH key is correct or not by calculating SSH key fingerprint. SSH daemon also checks if ssh key is expired.  If the SSH key is correct, it allows the user to log in without asking username or password.

An example for user bob is the following:

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDJlG20rYTk4o\
k+xFjkPHYp/R0LfJqEYDLXA5AJ49w3DvAWLrUg+1CpNq76WS\
qmQBmoG9jgbcAB5ABGdswdeMQZHilJcu29iJ3OKKv6SlCulAj1t\
HymwtbdhPuipd2wIDAQAB

#### <mark style="color:green;">**What is the purpose of SSH authorized\_keys file**</mark>

ssh authorized\_keys file is private. The ssh authorized\_keys file should be placed in a directory which is only accessible by the user. For example, the \~/.ssh directory.

ssh authorized\_keys file permissions should be set to 600 which means that only the user who owns the file can read and write to it.

ssh server daemon usually looks into ssh authorized\_keys file for ssh key fingerprint. ssh authentication protocol uses ssh keys to verify that the user is authorized to login.

#### <mark style="color:green;">where is the SSH authorized\_keys file located?</mark>

The authorized\_keys file is located in the .ssh directory. This directory is located in the user’s home directory. To add an SSH public key to the authorized\_keys file, you can use the ssh-keygen command on client side.

This command will generate an SSH key pair. The public key can be added to the authorized\_keys file on server side. You can also add an SSH public key to the authorized\_keys file manually. To do this, you will need to edit the file using a text editor.

#### <mark style="color:green;">How to add multiple keys from different accounts to SSH authorized\_keys file?</mark>

You can add multiple keys from different accounts to your authorized\_keys file by concatenating the files together. For example, if you have two files named id\_rsa.pub and id\_dsa.pub, you would type: cat id\_rsa.pub id\_dsa.pub >> \~/.ssh/authorized\_keys

#### <mark style="color:green;">FAQ about SSH authorized\_keys file</mark>

<mark style="color:green;">**What is the best way to enable SSH login without password?**</mark>

The best way to enable SSH login without password is to use an SSH key. SSH keys are more secure than passwords, and they can be used to authenticate with multiple accounts on different systems.

You can use the ssh-keygen command to generate an SSH key. For example, if you want to generate an RSA key, you would type: <mark style="color:green;">`ssh-keygen -t rsa`</mark>

<mark style="color:green;">**Why is the ssh public key not working for me when trying to log in?**</mark>

There could be a number of reasons why your ssh public key is not working. Make sure that you are using the correct key, and that the key has been added to the authorized\_keys file on the server.

<mark style="color:green;">**Is it possible to use a public and private key with one account on different systems?**</mark>

Yes, it is possible to use a public and private key with one account on different systems. You will need to generate a separate key for each system, and add the public key to the authorized\_keys file on each system.\


{% embed url="https://www.howtouselinux.com/post/ssh-authorized_keys-file" %}
