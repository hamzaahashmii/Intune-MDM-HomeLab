# Lessons learned

The short version. Full symptom-based guide: [troubleshooting.md](troubleshooting.md).

| Day | Lesson |
| --- | --- |
| 1 | Keep ISOs local, take snapshots before big changes, 8 GB RAM is tight – close other apps. |
| 2 | Turn recurring billing **off** right after starting a trial; protect the only admin with MFA + a backup method. |
| 3 | Assign licenses from the license side; dynamic groups and CA need Entra ID P1+. |
| 4 | **Join** (company) ≠ **register** (personal). Only joined devices offer company sign-in. |
| 5 | Compliance only reports. Default "no policy = Not compliant". VM TPMs can't do health attestation. |
| 6 | One setting, one place – the baseline causes conflicts. Check Included vs Excluded. Reports lag; test on the device. |
| 7 | Replace security defaults with your own MFA policy before anything else. Test blocking rules in Report-only. The Intune Management Extension is needed for Store/Win32 apps. |
| 8 | Offboarding order: block + revoke → wipe → licenses. A wiped device must enroll again (Autopilot automates it). Snapshots and resets need lots of free disk space. Never "un-wipe" a device. |
