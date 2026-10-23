# Troubleshooting guide

Every problem hit in this lab, grouped by where it shows up: **Symptom → Likely cause → How to check → Fix**.
General rule: check the **device itself** before assuming a policy is broken – Intune reports often lag behind reality.

## First checks for almost anything

1. Is the device **running**, with a user signed in? A paused/saved/off VM can't check in.
2. Is the **clock** right? (Settings > Time & language > Set time automatically > Sync now)
3. Is the policy assigned to **Included** groups, not Excluded?
4. Force a check-in: Intune device > **Sync**, or **restart** the device; press Cmd/Ctrl + R in the portal.
5. Compare device vs Intune: *Access work or school > Info* (last sync), `dsregcmd /status` (join state).

## VirtualBox and the host Mac

| Symptom | Likely cause | How to check | Fix |
| --- | --- | --- | --- |
| ISO greyed out | iCloud placeholder file | Cloud icon | Move the real file to a local folder |
| VM "Aborted" / VirtualBox crashes | Out of memory or disk | Activity Monitor, `df -h /` | Close apps, free 20+ GB, restart the Mac |
| `NS_ERROR_FAILURE`, "application will now terminate" | Disk almost full / stuck process | `df -h /`, Activity Monitor → VBox | Force quit (Option+Cmd+Esc), free space, restart |
| Disk space drops during a Windows reset | Post-snapshot changes go into a growing differencing disk | `df -h /` while running | Stop VM; restore snapshot **without** saving current state |
| "You must specify a machine to start, using the command line" | Opened *VirtualBoxVM* instead of *VirtualBox* | App name | Open VirtualBox from Applications |
| Keyboard dead on BitLocker recovery screen | Pre-boot keyboard not connected yet | — | Click into VM, Machine > Reset, or Input > Keyboard > Soft Keyboard |
| Passwords "don't match" in the VM | Invisible typos / layout differences | Eye icon, ENG/DEU in taskbar | Letters and numbers only, verify with the eye icon |
| USB stick not visible in Windows | USB passthrough not set up | Device Manager > Disk drives | Extension Pack + USB controller, or rely on *Succeeded* |

## Tenant, licenses, accounts

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| *Manage product licenses* shows nothing | Bulk panel doesn't load | Billing > Licenses > product > + Assign licenses |
| Dynamic membership not available | Entra ID Free | Start Entra ID P2 trial (Marketplace search → item labelled *Trial*) |
| Marketplace shows only paid plans | Trials not on front page | Use search; never click *Buy* |
| Can't sign in as another user in the browser | Admin session reused | Private window / other browser, *Use another account* |

## Enrollment and joining

| Symptom | Likely cause | How to check | Fix |
| --- | --- | --- | --- |
| No **Other user** on sign-in screen | Device **registered**, not joined (email typed in Connect box) | *Work or school account* instead of *Connected to … Entra ID*; Intune ownership Personal | Disconnect → Connect → link **Join this device to Microsoft Entra ID** |
| Other user hidden after policies arrive | Baseline changes sign-in screen | — | Insert Ctrl-Alt-Del |
| Sync asks to sign in, last check-in stuck | Cloud token expired | `dsregcmd /status` → AzureAdPrt | Sign in again, complete MFA |
| "Allow my organization to manage your device" | Standard prompt on re-sign-in | — | OK, then check for duplicate devices |
| "Notifying device: Error" | Push notification didn't reach VM | Sync status window | Sync from device or restart |

## Compliance and configuration

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| "No device compliance found" | First report takes 15–30 min | Wait, sync, restart |
| Secure Boot rule = Error | Health attestation fails with virtual TPM | Remove rule in VM labs |
| Still compliant right after changing a rule | Evaluation comes after sync | Watch Sync status, refresh |
| Profile does nothing | Group under **Excluded** | Move to Included |
| Several profiles in **Conflict** | Same setting, different values (often the baseline) | Set it to *Not configured* in one place |
| Report shows 1 profile / 0 check-ins | Report lag after offline period | Trust Sync status + on-device tests |
| Setting not found | Long search words, child settings | Short keywords, browse category, set parent first |
| BitLocker "waiting for activation" | TPM protector not added yet | Restart; don't turn it on manually |
| Local account forced to change password | Password length rule applies to local accounts | Letters+numbers; manage with Windows LAPS |

## Conditional Access

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| No MFA prompt | Policy never saved | CA Overview > Policy snapshot; recreate, tick the lock-out warning |
| CA column "Not applied" | Report-only policies not shown there | Open sign-in > Report-only tab |
| "Set up your device to get access" | That **is** the compliant-device block | Working; close enrollment with restrictions |

## Apps

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Store/Win32 apps never install | Intune Management Extension missing (`C:\Program Files (x86)\Microsoft Intune Management Extension`) | Sync and restart |
| App never arrives | App never created | Recreate, wait for *Successfully created* |
| "Application is not available" | Store can't supply that app | Other app or package as Win32 |
| Available app fails once | Temporary | Retry in Company Portal |

## Updates and lifecycle

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| Remote restart didn't happen | User dismissed it | Update ring deadlines |
| Wipe *Pending*, actions greyed out | Device hasn't checked in | Keep device on, restart or sign in |
| BitLocker recovery screen | TPM saw a startup change | Match Key ID in Intune/Entra, type 48 digits |
| "Couldn't remove all personal files" | Some files not cleaned | OK internally; wipe again / Erase device before a laptop leaves |
| Device gone from Intune after wipe | Only managed devices are listed | Expected; re-enrolls on setup (Autopilot keeps registration) |
| Device orphaned after snapshot restore | Snapshot "un-wiped" the VM | Delete stale entries, restore earlier snapshot, join again |
