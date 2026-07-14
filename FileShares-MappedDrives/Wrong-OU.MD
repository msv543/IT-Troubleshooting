# Wrong OU Drive Map Placement

## Problem

Users in the Sales organizational unit are supposed to receive the S: network drive through Group Policy Preferences. After logging in, the drive does not appear in File Explorer even though Group Policy is updating successfully.

## Symptoms
- Sales drive is missing from File Explorer.
- gpudate /force completes successfully.
- No errors are displayed during logon.
- Other group polices apply normally.
- Shared folder is accessible manually using UNC path.
- Running gpresult /r shows the Sales Drive Mapping GPO applied.

## Investigation

1. Logged in as Sales1 user.
2. Confirmed the Sales Drive was missing.
3. Verified the shared folder could be opened manually using: \\FILESERVER\Sales Drive.
4. Ran gpupdate /force and restarted the PC.
5. Ran gpresult /r and verified the Sales Drive Mapping GPO was applied.
6. Opened Group Policy Management in Domain Controller.
7. Edited the 'Sales Drive Map' and navigated to: User Configuration -> Preferences -> Windows Settings -> Drive Maps
8. Verified the drive letter, share path, and security filtering were correct.
9. Discovered the mapping item had been configured with Item-level targeting that referenced the wrong Active Directory OU, preventing the drive from being created from the current user.

## Commands Used
```
gpupdate /force
gpresult /r
net use
```

## Root Cause

The Drive Mapping preference contained an incorrect Item-level Targeting configuration, causing the preference item to be skipped even though the GPO itself was successfully applied.

As a result, the drive mapping policy never processed for Sales users.

## Resolution
1. Corrected the Item-level targeting by removing it.
2. Saved the GPO.
3. Forced a policy refresh by using: gpupdate /force
4. Logged off and back on.

## Verification
- Sales drive appeared automatically.
- Drive letter matched with GPO configuration.
- Users could browse and create files.
- net use displayed the mapped drive.
- gpresult /r continued showing the GPO was applied.
- The mapped drive persisted after subsequent logons.

