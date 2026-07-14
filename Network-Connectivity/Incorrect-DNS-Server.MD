# Incorrect DNS Server

## Problem

A Windows 11 client was unable to access websites or domain resources because it was configured with an incorrect DNS server address.

## Symptoms

- Internet websites would not load.
- ping google.com failed.
- nslookup google.com failed.
- Domain resources could not be located.
- ping 8.8.8.8 was successful. indicating basic network connectivity.

## Investigation

1. Verified the client's TCP/IP configuration using: ipconfig /all
2. Tested DNS resolution using: nslookup
3. Confirmed the issue was limited to name resolution by successfully pinging a public IP address.

## Commands Used

```cmd
ipconfig /all
nslookup google.com
ping google.com
ping 8.8.8.8
ipconfig /flushdns 
ipconfig /renew

## Root Cause

The client was configured with an incorrect DNS server address, preventing hostname resolution.

## Resolution

Updated the preferred DNS Server to the correct internal DNS server provided by the Domain Controller.

## Verification

- Successfully resolved hostnames using 'nslookup'
- Successfully pinged 'google.com'
- Internet browsing functionality was restored.
- Domain resources were accessible again.
