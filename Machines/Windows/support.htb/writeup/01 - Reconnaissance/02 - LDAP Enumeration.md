---
title: LDAP Enumeration
tags: [recon, ldap, active-directory]
---

# LDAP Enumeration

## User enumeration
```bash
ldapsearch -x -H ldap://192.168.60.76 -b "dc=visual,dc=local" "(objectclass=user)" sAMAccountName | grep sAMAccountName
```

Natijada `visual.local` userlari, jumladan `park.ian`, `hall.noa`, `roy.ada` va boshqalar ko‘rindi.

## NetExec LDAP
```bash
nxc ldap 192.168.60.76 -u '' -p '' --users
```

Screenshotda `visual.local` va 20 ta domain user enumeration qilingani ko‘rinadi. Lab outputida `park.ian` uchun password qiymati ham ochiq ko‘ringan. [[../02 - Initial Access/01 - Discovered Credentials]]

![[02 - LDAP Enumeration.png]]
