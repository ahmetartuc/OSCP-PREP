# Kerberos Exploitation and Enumeration Cheatsheet

## Nmap Scripts

```bash
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='test.local'" 192.168.1.1
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='test.local'",userdb=/usr/share/seclists/Usernames/Names/names.txt 192.168.1.1
