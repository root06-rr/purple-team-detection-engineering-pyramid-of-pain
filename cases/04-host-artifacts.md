# Case 04: Host artifacts

**Pyramid tier:** Host Artifacts  
**Sample:** `sample4.exe`  
**Defensive focus:** Windows Defender registry activity

## Lab activity

The notes describe sandbox activity in which `sample4.exe` modified the Windows Defender Real-Time Protection registry setting. The recorded value was `DisableRealtimeMonitoring = 1`.

The registry path recorded in the notes is:

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection
```

## Defensive response recorded in the notes

A Sysmon registry detection rule was created to look for a change to the `DisableRealtimeMonitoring` value. The rule is stored at [win_defender_realtime_tampering.yml](../rules/win_defender_realtime_tampering.yml).

The rule uses Event ID 13 and checks the registry target and value details. Its exact field values still need to be compared with the event data produced by the lab source.

## MITRE ATT&CK reference

The original notes map this activity to Defense Evasion, technique `T1562.001`.

## Related files

- [Registry rule](../rules/win_defender_realtime_tampering.yml)
- [Indicator record](../iocs/blocked_indicators.md)
- [Evidence files](../evidence/)

## What this case shows

This case moves beyond a file or network indicator and focuses on a change to a security setting on the host.
