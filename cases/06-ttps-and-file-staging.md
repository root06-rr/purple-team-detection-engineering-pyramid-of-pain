# Case 06: TTPs and file staging

**Pyramid tier:** TTPs  
**Sample:** `sample6.exe`  
**Defensive focus:** Living-off-the-land activity and file staging

## Lab activity

The notes describe `sample6.exe` spawning multiple child `cmd.exe` processes. One child process was recorded as writing reconnaissance output to:

```text
%temp%\exfiltr8.log
```

The notes describe this as a living-off-the-land technique because the activity used a native Windows command interpreter.

## Defensive response recorded in the notes

A Sigma rule was authored to look for activity involving `exfiltr8.log` under the user's temporary directory. The rule is stored at [lotl_cmd_temp_data_staging.yml](../rules/lotl_cmd_temp_data_staging.yml).

The rule currently uses Sysmon Event ID 2 while describing file creation or modification. Event ID 2 records file creation time changes. The event ID and field selection need to be checked against the source telemetry before the rule is treated as a file creation detection.

## MITRE ATT&CK reference

The original notes map the activity to Exfiltration, tactic `TA0010`, and Data Staged, technique `T1074.001`.

## Related files

- [File staging rule](../rules/lotl_cmd_temp_data_staging.yml)
- [Indicator record](../iocs/blocked_indicators.md)
- [Evidence files](../evidence/)

## What this case shows

This case focuses on a behavior rather than a specific malware hash or external destination. The repository contains a draft rule, but it does not yet include a documented test showing that the rule matches the intended event.
