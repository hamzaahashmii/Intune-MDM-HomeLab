# Microsoft Intune MDM Home Lab

A hands-on lab covering one full Mobile Device Management (MDM) lifecycle in **Microsoft Intune** and **Microsoft Entra ID**: tenant setup, enrollment, compliance, configuration, Conditional Access, app deployment, updates, offboarding and onboarding – with every problem I hit and how I fixed it.

## Lab diagram

```
 Admin laptop (macOS)                        Microsoft cloud (lab tenant)
 ┌────────────────────────────┐            ┌──────────────────────────────────┐
 │ Browser (separate profile) │ ─────────► │ Microsoft 365 admin center       │
 │                            │            │   licenses, billing, trials      │
 │ VirtualBox                 │            │ Entra admin center               │
 │  └─ Windows 11 Enterprise  │ ◄────────► │   users, groups, CA, sign-in logs│
 │     VM ("employee laptop") │  enrolled  │ Intune admin center              │
 └────────────────────────────┘            │   devices, policies, apps        │
                                           └──────────────────────────────────┘
```

## Tools

| Part | Role |
| --- | --- |
| MacBook Pro (Intel, 8 GB) | IT admin computer |
| VirtualBox | Runs the test device |
| Windows 11 Enterprise evaluation VM (4 GB, 2 CPU, TPM 2.0) | Employee laptop |
| Microsoft Intune Plan 1 trial | MDM |
| Microsoft Entra ID P2 trial | Identity, dynamic groups, Conditional Access |

## Contents

| Day | Topic | Notes |
| --- | --- | --- |
| 1 | Lab setup: VirtualBox, Windows 11 VM, snapshots | [01-lab-setup.md](01-lab-setup.md) |
| 2 | Intune trial, tenant, admin MFA, billing safety | [02-intune-trial-tenant.md](02-intune-trial-tenant.md) |
| 3 | Users, licenses, assigned and dynamic groups | [03-users-groups-licenses.md](03-users-groups-licenses.md) |
| 4 | Entra join and Intune enrollment | [04-enrollment.md](04-enrollment.md) |
| 5 | Compliance policies (and breaking them on purpose) | [05-compliance.md](05-compliance.md) |
| 6 | Configuration profiles, BitLocker, security baseline, conflicts | [06-configuration.md](06-configuration.md) |
| 7 | Conditional Access (MFA, compliant device) and apps incl. Win32 packaging | [07-conditional-access-apps.md](07-conditional-access-apps.md) |
| 8 | Update rings, remote actions, offboarding and onboarding | [08-updates-lifecycle.md](08-updates-lifecycle.md) |
| 9 | Troubleshooting practice: logs and real cases | [09-troubleshooting-practice.md](09-troubleshooting-practice.md) |
| — | **Troubleshooting guide** (symptom → cause → check → fix) | [troubleshooting.md](troubleshooting.md) |
| — | Lessons learned | [lessons-learned.md](lessons-learned.md) |

## Skills covered

- Microsoft 365 tenant setup, trials and licensing (Intune Plan 1, Entra ID P1/P2, M365 E3/E5, Business Premium)
- Entra ID users, assigned and dynamic device groups, device join settings, sign-in logs
- Entra join vs registration, automatic MDM enrollment, Autopilot concepts
- Compliance policies, noncompliance actions, compliance reporting
- Settings catalog profiles, silent BitLocker with Entra key escrow, security baselines, conflict resolution
- Conditional Access: replacing security defaults, MFA, require compliant device, Report-only testing
- App deployment: Store apps, Required vs Available, Company Portal, **Win32 packaging** (IntuneWinAppUtil, install/uninstall commands, detection rules)
- Update rings, feature update policies, remote actions, offboarding and re-onboarding
- Troubleshooting with `dsregcmd /status`, sync status, device action reports, BitLocker recovery

> Tenant names, email addresses, phone numbers and recovery keys are removed or blurred in all notes and screenshots.
