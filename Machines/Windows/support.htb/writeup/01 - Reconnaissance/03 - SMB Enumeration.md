---
title: SMB Enumeration
tags: [recon, smb]
---

# SMB Enumeration

## Command
```bash
nxc smb 192.168.60.76 -u 'park.ian' -p '<LAB_PASSWORD>' --shares
```

## Kuzatilgan sharelar

| Share | Permission | Izoh |
|---|---|---|
| `ADMIN$` | — | Remote Admin |
| `C$` | — | Default share |
| `IPC$` | READ | Remote IPC |
| `NETLOGON` | READ | Logon server share |
| `SYSVOL` | READ | Logon server share |

![[03 - SMB Enumeration.png]]
