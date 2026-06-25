# Windows Server RDS Learning Path 60 — Troubleshoot RDS Profile Problems

**Level:** Expert · **Module:** 60/70

## Goal
Diagnose temporary profiles, slow logons, profile locks, corruption and storage failures.

## Workflow
1. Record user, Session Host, timestamp and exact symptom.
2. Review User Profile Service and RDS events.
3. Verify profile-share DNS, network path, permissions and free space.
4. Inspect profile container/disk attachment and whether the profile is loaded elsewhere.
5. Compare with a new test user.
6. Back up user data before repair or recreation.
7. Measure first and repeat logon times after remediation.

```powershell
Get-WinEvent -LogName Application -MaxEvents 200 |
 Where-Object ProviderName -match 'User Profile'
Get-CimInstance Win32_UserProfile |
 Select-Object LocalPath,Loaded,Status,LastUseTime
Get-PSDrive C
Get-SmbSession
```

## Evidence
Store events, share/ACL checks, profile/container state, free space, backup, corrective action and logon timing under `evidence/`.

## Troubleshooting
Temporary profiles require finding the storage, permission, lock or corruption cause. Do not delete a user profile before preserving data.

## Security
Profile stores contain sensitive data; use least privilege and sanitize paths/usernames in public evidence.

## Rollback
Restore the backed-up profile data and previous collection profile configuration if repair fails.

## Next
`Windows-Server-RDS-Learning-Path-61-Create-an-RDS-Health-Assessment`
