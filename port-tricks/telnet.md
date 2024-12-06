# Telnet Exploitation and Enumeration Cheatsheet

## Nmap Vulnerability Script

```bash
nmap -n -sV -Pn --script "*telnet* and safe" -p 23 192.168.1.1
```

## Banner Grabbing

```bash
nc -vn 192.168.1.1 23
```

## Brute Force Telnet with Hydra

```bash
hydra -C /usr/share/seclists/Passwords/Default-Credentials/telnet-betterdefaultpasslist.txt telnet://192.168.1.1
hydra -C /usr/share/seclists/Passwords/Default-Credentials/telnet-phenoelit.txt telnet://192.168.1.1
```

## Common Telnet Configuration File Locations

```
/etc/inetd.conf
/etc/xinetd.d/telnet
/etc/xinetd.d/stelnet
