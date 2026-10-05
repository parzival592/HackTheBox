---
title: Attack Path
tags: [cybersecurity, active-directory, lab]
---

# Attack Path

```text
VISUAL-DC1 (192.168.60.76)
        │
        ├── Nmap service discovery
        │
        ├── LDAP enumeration
        │      └── domain userlar topildi
        │             └── lab output ichida park.ian credential ko‘rindi
        │
        ├── park.ian bilan SMB authentication
        │      └── sharelar enumeration qilindi
        │
        ├── BloodHound collection
        │      └── AD relationshiplar xaritalandi
        │
        ├── hall.noa
        │      └── ForceChangePassword relationship kuzatildi
        │             └── labda hall.noa password o‘zgartirildi
        │
        ├── Domain Admins relationship / membership operation
        │
        └── DCSync / secretsdump
               └── SAM, LSA secrets, NTDS.DIT credential material
```

## Muhim eslatma

Screenshotlarda aniq ko‘rinmagan graph node yoki relationship nomlarini taxmin qilib qo‘ymadim.

## Bosqichlar

1. [[01 - Reconnaissance/01 - Nmap Scan]]
2. [[01 - Reconnaissance/02 - LDAP Enumeration]]
3. [[01 - Initial Access/01 - Discovered Credentials]]
4. [[01 - Reconnaissance/03 - SMB Enumeration]]
5. [[02 - Initial Access/02 - BloodHound Collection]]
6. [[03 - BloodHound/02 - Hall Noa]]
7. [[03 - BloodHound/03 - ForceChangePassword]]
8. [[04 - Privilege Escalation/01 - Password Change]]
9. [[04 - Privilege Escalation/02 - Domain Admin Membership]]
10. [[05 - Domain Compromise/01 - DCSync and SecretsDump]]
