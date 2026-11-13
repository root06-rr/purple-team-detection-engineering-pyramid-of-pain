# Case 01: Hash values

**Pyramid tier:** Hash Values  
**Sample:** `sample1.exe`  
**Defensive focus:** File triage and hash-based blocking

## Lab activity

The lab notes describe an untrusted Windows executable named `sample1.exe`. The file was submitted to a malware analysis sandbox instead of being run on the simulated workstation. The sandbox report identified a 64-bit Windows executable with Metasploit markers and suspicious outbound network activity.

## Indicator recorded

The SHA-256 value recorded in the repository is:

```text
9c550591a25c6228cb7d74d970d133d75c961ffed2ef7180144859cc09efca8c
```

## Defensive response recorded in the notes

The hash was added to the EDR IOC blocklist. The notes describe this as preventing the sample from executing on the simulated endpoint.

## Indicator screenshot

- [sample1.exe sandbox triage](../evidence/02_case1_sample1_sandbox_triage.png)

## Evidence screenshot

- [EDR hash blocklist](../evidence/03_case1_edr_hash_blocklist.png)

## What this case shows

A file hash is useful for identifying a known file, but a changed binary can have a different hash. The next case records the move from a file indicator to network infrastructure.
