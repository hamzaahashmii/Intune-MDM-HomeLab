# Day 1 – Lab setup

**Goal:** a working Windows 11 Enterprise VM that acts as an employee's company laptop.

**Why:** the real Mac is never enrolled. All MDM testing happens on a VM that can be reset with a snapshot.

## Steps

1. Installed VirtualBox (macOS / Intel hosts version).
2. Downloaded the Windows 11 Enterprise evaluation ISO (64-bit, English) to a **local** folder (not iCloud).
3. Created the VM **Win11-Lab**: 4096 MB memory, 2 processors, EFI, TPM 2.0, Secure Boot.
   - *Why EFI, TPM 2.0 and Secure Boot:* Windows 11 requires them, and the Day 5 compliance policy checks Secure Boot.
4. Installed Windows manually (unattended install unticked) to see every setup screen.
5. Chose "I don't have internet" and created the local account `labadmin`.
6. Fixed internet after setup and checked activation: Settings > System > Activation = Active.
7. Took the snapshot **"Clean Windows - before Intune"** (Machine > Take Snapshot).

## VirtualBox controls (Mac)

| Keys | Action |
| --- | --- |
| Left Command | Host key, releases the mouse |
| Left Command + F | Full screen on/off |
| Left Command + R | Resets the VM (avoid) |
| Left Command + Q | Quits (avoid) |
| Red close button > Save the machine state | Stop for the day |

## Golden rules

- Never enroll the real Mac.
- Use a personal email and a separate browser profile, never a work account.
- Take a snapshot before every big change.
- Close other Mac apps while the VM runs (8 GB is tight).
