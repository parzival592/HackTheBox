---
title: BloodHound Collection
tags: [bloodhound, active-directory, enumeration]
---

# BloodHound Collection

```bash
bloodhound-python -u 'park.ian' -p '<LAB_PASSWORD>' -d visual.local -ns 192.168.60.76 -c All
```

## Natija
- 1 domain
- 1 computer
- 24 users
- 52 groups
- 2 GPOs
- 2 OUs
- 19 containers
- 0 trusts

Kerberos TGT olish screenshotda muvaffaqiyatsiz bo‘lgan va tool NTLM authentication'ga fallback qilgan. Collection muvaffaqiyatli tugagan.

![[04 - BloodHound Collection.png]]
