# Directory Enumeration with Dirsearch Cheatsheet

## Common Parameters

| **Parameter** | **Description** |
| --- | --- |
| `-i` | Include status codes |
| `-x` | Exclude status codes |
| `-e` | Extensions |
| `-w` | Wordlist |

## Example Usage

```bash
dirsearch -u http://192.168.1.1 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt -e php,txt,zip -i 200 -x 400
