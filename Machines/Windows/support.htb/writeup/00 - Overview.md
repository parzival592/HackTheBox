---
title: Machine Najot — Umumiy ko‘rinish
tags: [cybersecurity, active-directory, lab]
---

# Machine Najot — Umumiy ko‘rinish

> [!NOTE]
> Ushbu vault berilgan screenshotlar va text fayllar asosida tartiblangan lab yozuvidir. U o‘quv maqsadidagi authorized lab muhiti uchun mo‘ljallangan.

## Target

| Element | Qiymat |
|---|---|
| Host | `VISUAL-DC1` |
| IP | `192.168.60.76` |
| Domain | `visual.local` |
| OS | Windows Server 2022 Build 20348 |
| Asosiy servislar | DNS, Kerberos, RPC, LDAP, SMB, HTTPAPI |

## Yuqori darajadagi yo‘l

`Nmap` → `LDAP enumeration` → `park.ian` credential → `SMB enumeration` → `BloodHound` → `hall.noa` / `ForceChangePassword` → password change → group membership yo‘li → `Domain Admins` → `DCSync / secretsdump`

## Evidence

- [[01 - Attack Path]]
- [[01 - Reconnaissance/01 - Nmap Scan]]
- [[01 - Reconnaissance/02 - LDAP Enumeration]]
- [[02 - Initial Access/01 - Discovered Credentials]]
- [[03 - BloodHound/03 - ForceChangePassword]]
- [[05 - Domain Compromise/01 - DCSync and SecretsDump]]
- [[06 - Credentials/Credentials]]

## Screenshotlar

Barcha berilgan screenshotlar [[09 - Screenshots/]] ichida saqlangan.
