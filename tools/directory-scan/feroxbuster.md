# Directory Enumeration with Feroxbuster

## Common Parameters

| **Parameter** | **Description** |
| --- | --- |
| `-s` | Selected status codes |
| `-x` | Extensions |
| `-w` | Wordlist |

## Example Usage

```bash
feroxbuster -u http://192.168.1.1 -s 200 -x php,txt,zip -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
