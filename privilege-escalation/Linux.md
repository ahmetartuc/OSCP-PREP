# Linux Privilege Escalation Cheatsheet

## General Information and Information Gathering

```bash
id  ## Display user group information.
ls -la /etc/passwd  ## Check if the passwd file has write permissions.
env   ## Display environment variables, sometimes passwords can be stored here.
hostnamectl  ## Get system and hardware information.
ifconfig  ## View network configuration.
cat /etc/issue  ## Display operating system version.
cat /etc/os-release  ## Get more detailed OS information.
uname -a  ## Display the kernel version, useful for checking kernel exploits.
sudo -l  ## View sudo privileges.
ps aux | grep -i 'root' --color=auto  ## Check which root processes are running.
ip a  ## Display network connections, check for subnets.
routel  ## Show routing table.
ss -ntlup  ## Display TCP and UDP socket information.
cat /etc/iptables/rules.v4  ## Show network traffic rules.
```

## Scheduled Tasks (Cron Jobs)

```bash
ls -lah /etc/cron*  ## List all cron-related directories and files.
crontab -l  ## Show the current user's crontab.
sudo crontab -l  ## Show the root user's crontab.
crontab -u root -l  ## Display the crontab for a specific user.
grep "CRON" /var/log/syslog  ## Check cron logs.
```

## File and Permission Checks

```bash
dpkg -l  ## Display installed packages.
cat .bashrc  ## Check the user's bash configuration file.
find / -writable -type d 2>/dev/null  ## Find writable directories.
find / -perm -u=s -type f 2>/dev/null  ## Find files with SUID bit set.
find / -perm -g=s -type f 2>/dev/null  ## Find files with SGID bit set.
find / -perm /4000 2>/dev/null  ## Find all SUID files.
cat /etc/fstab  ## Check mounted file systems.
mount  ## Display current mount information.
lsblk  ## Get a list of connected disks.
lsmod  ## Show loaded kernel modules.
```

## SQL, SSH, and File Discovery

```bash
grep -Ri 'sql' . --color=auto  ## Find SQL connection information.
grep -Ri 'db' . --color=auto  ## Search for database references.
ls -lsaR /home/  ## Check for SSH keys.
ls -lsaht /bin/ | grep -i 'ftp' --color=auto  ## Find file transfer tools.
```

## Privilege Escalation and Network Analysis

```bash
getcap -r / 2>/dev/null  ## Check for high-privileged files with capabilities.
netstat -unlp  ## Show only TCP connections.
netstat -tunlp  ## Show both TCP and UDP connections.
openssl passwd -1  ## Generate a new hashed password.
```

## File Permissions and Sensitive Information Discovery

```bash
find / -type f -perm 777 2>/dev/null  ## World-writable files.
find / -type f -perm /4000 2>/dev/null  ## SUID bit set files.
find / -perm -222 -type f 2>/dev/null  ## Writable files.
find / -writable -type d 2>/dev/null  ## Writable directories.
cat .bashrc  ## Might contain sensitive information.
env  ## Check environment variables.
watch -n 1 "ps -aux | grep pass"  ## Monitor active processes for passwords.
```

## SUDO / SUID / Capabilities

```bash
sudo -l  ## Show the user's sudo privileges.
find / -perm -u=s -type f 2>/dev/null  ## SUID bit set files.
getcap -r / 2>/dev/null  ## Check file capabilities.
```

## NFS (Network File System)

```bash
cat /etc/exports  ## View NFS shares.
showmount -e <target IP>  ## Display NFS shares on the target IP.
mount -o rw <targetIP>:<share-location> <directory>  ## Mount NFS shares.
```

## TTY Shell

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'  ## Spawn a better interactive shell.
export TERM=xterm-256color  ## Set terminal type.
Ctrl+Z  ## Suspend the shell to the background, then bring it back.
stty raw -echo; fg; reset  ## Reopen and configure the shell.
```

## Shell Spawning

```bash
/bin/sh -i  ## Spawn an interactive `/bin/sh` shell.
/bin/bash -i  ## Spawn an interactive `/bin/bash` shell.
perl -e 'exec "/bin/sh";'  ## Launch a shell using Perl.
awk 'BEGIN {system("/bin/bash -i")}'  ## Launch a shell using Awk.
