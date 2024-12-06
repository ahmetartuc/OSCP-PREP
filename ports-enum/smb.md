# SMB Exploitation and Enumeration Cheatsheet

## Nmap Scripts

```bash
nmap --script smb-vuln-*.nse -p 139,445 192.168.1.1
nmap --script=smb-vuln\* -p 445 192.168.1.1
nmap --script "safe or smb-enum-*" -p 445 192.168.1.1
