# hashcat

## Normal Cracking

```bash
hashcat hash /usr/share/wordlists/rockyou.txt
```

## Hash Type Cracking

```bash
hashcat -m 1998 hash /usr/share/wordlists/rockyou.txt
```

## Common Hash Types

| **ID**  | **Hash Type**                |
|---------|------------------------------|
| 1000    | NTLM                        |
| 5600    | NetNTLMv2                   |
| 13400   | KeePass (kdbx file)         |
| 18200   | Kerberos 5 (AS-REP)         |
| 13100   | Kerberos 5 (TGS-REP)        |
| 22911   | RSA/DSA/EC/OpenSSH ($0$)    |
| 22921   | RSA/DSA/EC/OpenSSH ($6$)    |
| 22931   | RSA/DSA/EC/OpenSSH ($1, $3$)|
| 22941   | RSA/DSA/EC/OpenSSH ($4$)    |
| 22951   | RSA/DSA/EC/OpenSSH ($5$)    |

## Cracking with Rules

```bash
hashcat -m 13100 hash /usr/share/wordlists/rockyou.txt -r /usr/share/hashcat/rules/rockyou-30000.rule --force
