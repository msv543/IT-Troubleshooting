# Windows Firewall Blocking Internet Traffic Troubleshooting Lab

## Problem

A Windows 11 client was unable to access the internet because a Windows Defender Firewall outbound rule was blocking network traffic.

## Symptoms

- Unable to browse websites.
- Applications requiring internet access failed to connect.
- Network adapter appeared connected.
- IP configuration was correct.
- Internal network resources remained accessible.

## Investigation

Verified the client's network configuration using:

```cmd
ipconfig /all
```

Confirmed the client had a valid IP address, subnet mask, default gateway, and DNS server.

Reviewed Windows Defender Firewall with Advanced Security (`wf.msc`) and discovered a custom outbound rule blocking internet traffic.

## Commands Used

```cmd
ipconfig /all
wf.msc
ping 192.168.100.10
ping 8.8.8.8
```

## Root Cause

A custom outbound Windows Defender Firewall rule was preventing internet traffic from leaving the workstation.

## Resolution

Disabled or removed the blocking outbound firewall rule.

## Verification

Verified internet connectivity by:

```cmd
ping 8.8.8.8
ping google.com
```

Successfully browsed external websites and confirmed applications could access the internet.
