# Case 06: TTPs and file staging

**Pyramid tier:** TTPs  
**Sample:** `sample6.exe`  
**Defensive focus:** Living-off-the-land activity and file staging

## Lab activity

The notes describe `sample6.exe` spawning multiple child `cmd.exe` processes. One child process was recorded as writing reconnaissance output to:

```text
%temp%\exfiltr8.log
```

The evidence screenshot shows `sample6.exe` as the parent process, three child `cmd.exe` processes, and PID 2312 creating the file.

## Defensive response recorded in the notes

A Sigma-style rule was authored to look for `cmd.exe` creating `exfiltr8.log` in the user's temporary directory. The rule is stored at [lotl_cmd_temp_data_staging.yml](../rules/lotl_cmd_temp_data_staging.yml).

The original rule used Sysmon Event ID 2 while describing file creation or modification. Event ID 2 records file creation time changes. I changed the draft to Event ID 11, which records file creation. The rule checks the creating process image and target filename.

The screenshot is a sandbox summary, not a raw Sysmon Event ID 11 record. The corrected rule still needs to be tested against the actual event fields. It also does not correlate the file event with the parent process. The case notes describe that process relationship, but the available screenshot does not provide the raw event records needed to build and test that correlation.

## MITRE ATT&CK reference

The original notes map the activity to Exfiltration, tactic `TA0010`, and Data Staged, technique `T1074.001`.

## Indicator screenshot

- [sample6.exe process lineage and file staging](../evidence/14_case6_sample6_process_lineage.png)

## Evidence screenshot

- [File staging Sigma rule](../evidence/15_case6_sigma_exfiltration_rule.png)

## What this case shows

This case focuses on a behavior rather than a specific malware hash or external destination. The rule now uses the Sysmon event type associated with file creation, but it has not been tested against a raw event.
