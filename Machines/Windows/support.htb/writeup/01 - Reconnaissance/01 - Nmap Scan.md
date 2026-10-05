---
title: Nmap Scan
tags: [recon, nmap]
---

# Nmap Scan

## Command
```bash
nmap -sCV 192.168.60.76 -T4
```

## Kuzatilgan servislar

| Port | Service | Kuzatuv |
|---:|---|---|
| 53 | DNS | Simple DNS Plus |
| 88 | Kerberos | Microsoft Windows Kerberos |
| 135 | MSRPC | Microsoft Windows RPC |
| 139 | NetBIOS-SSN | Microsoft Windows netbios-ssn |
| 389 | LDAP | AD LDAP, `visual.local` |
| 445 | SMB | Microsoft DS |
| 464 | kpasswd5 | Kerberos password service |
| 593 | ncacn_http | Windows RPC over HTTP |
| 636 | tcpwrapped | LDAPS bilan bog‘liq port |
| 3268 | LDAP | Global Catalog / AD LDAP |
| 3269 | tcpwrapped | Global Catalog TLS bilan bog‘liq port |
| 5985 | HTTP | Microsoft HTTPAPI 2.0 |

Nmap natijasida SMB message signing **enabled and required** ekani ko‘rsatilgan.

![[01 - Nmap Scan.png]]

Keyingi bosqich: [[02 - LDAP Enumeration]].
