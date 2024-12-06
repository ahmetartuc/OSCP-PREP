# Gobuster Enumeration Cheatsheet

## Common Parameters

| **Parameter** | **Description** |
| --- | --- |
| `-b` | Negative status codes |
| `-w` | Wordlist |
| `--timeout` | Timeout |
| `-x` | Extensions |

## Directory Enumeration Example

```bash
gobuster dir -u http://192.168.1.1 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 20 -b 400,404 -x php,txt,zip
```

## Subdomain Enumeration Example

```bash
gobuster dns -d ctf.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -t 20
