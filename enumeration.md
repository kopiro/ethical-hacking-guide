# Enumeration

## Ports

Port scanning is a method of determining which ports on a network are open and could be receiving or sending data.

It is also a process for sending packets to specific ports on a host and analyzing responses to identify vulnerabilities.

### TCP ports

A TCP complete scan with OS/version detection is the best thing to start with.

```sh
nmap -p- -sV -Pn -A -oA $RHOST
```

* `-p-` : Scan all ports
* `-sV` : Probe open ports to determine service/version info
* `-Pn` : Treat all hosts as online -- skip host discovery
* `-A` : Enable OS detection, version detection, script scanning, and traceroute

[https://nmap.org/](https://nmap.org/)

#### UDP ports

Sometimes is useful to inspect UDP ports as they can expose unsafe services; add `-sU` as parameter.

## HTTP

### Directories and files

Gobuster is a tool used to brute-force URIs (directories and files) in web sites.

[https://tools.kali.org/web-applications/gobuster](https://tools.kali.org/web-applications/gobuster)

```sh
WORDLIST=/usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
gobuster \
-k \
-w $WORDLIST \
-u $RHOST
```

## DNS

### Subdomains

Enumerate DNS information of a domain and to discover non-contiguous ip blocks.

```sh
dnsenum $RDOMAIN
```

### Domain

DMitry has the ability to gather as much information as possible about a host. Base functionality is able to gather possible subdomains, email addresses, uptime information, tcp port scan, whois lookups, and more.

```sh
dmitry $RDOMAIN
```

## SMB

SMBMap allows users to enumerate samba share drives across an entire domain.

```sh
smbmap $RHOST
```

Alternatively, with nmap:

```sh
nmap --script smb-enum-shares $RHOST
```