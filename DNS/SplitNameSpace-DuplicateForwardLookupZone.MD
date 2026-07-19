# Incorrect Forward Lookup Zone 

## Problem

Clients in the domain are experiencing Group Policy failures and intermittent domain controller discovery issues. Basic hostname resolution still works normally.

## Symptoms

- gpupdate /force fails.
- SYSVOL/NETLOGON access is incosistent.
- Ping dc1 works.
- nslookup dc1 works.
- A records resolve normally.
- No obvious DNS errors appear in basic tests.

## Investigation

1. Verified DNS server settings by running this command on PowerShell: ipconfig /all.
  - DNS Settings are correct.
2. Tested basic hostname resolution by runnning 3 commands:
```
nslookup dc1
ping dc1
ping fileserver
```
3. Tested DC Locator by running this command: nltest /dsgetdc:martinlab.local
  - "ERROR_NO_SUCH_DOMAIN"
4. On Domain Controller 1, Navigated to: Server Manager -> DNS -> Forward Lookup Zones.
5. Noticed two similar zones and one of them is incorrect.

## Root Cause

A second forward lookup zone was created with an incorrect name: martinlab.locall

## Resolution

1. Still on DC1, deleted martinlab.locall zone.
2. On PC1, flushed and re-registered the DNS.
3. Reset PC1.

## Verification

- Verified Hostname resolution by running: nslookup dc1 and ping dc1.
- Forcing group policy works successfully.
- DC Locator works successfully.


