# Wrong Default Gateway

## Problem
A Windows 11 client was unable to access external networks because the default gateway was configured incorrectly.

## Symptoms

- Unable to browse the internet.
- Could not ping external IP addresses.
- Able to communicate with devices on the local network.
- Domain Controller remained reachable.

## Investigation

1. Reviewed the client's IP configuration using ipconfig /all.
2. Observed that the Default Gateway was configured with an incorrect IP address.
3. Confirmed local connectivity by pinging the Domain Controller while external connectivity failed.

## Commands Used
```
ipconfig /all
route print
ping 192.168.100.10
ping 8.8.8.8
tracert 8.8.8.8
```

## Root Cause

The client was configured with an incorrect default gateway, preventing traffic from leaving the local subnet.

## Resolution

Corrected the Default Gateway to the VMware NAT gateway.

## Verification

- Successfully pinged external IP addresses.
- Traceroute completed successfully.
- Internet access was restored.
