# Detection rule review

This page records the review of the three YAML rule drafts against the Notion lab notes and the screenshots in this repository. The screenshots are the complete evidence set available for this project. They support the observed lab behavior and intended detection logic, but they do not provide raw event records for event-level testing.

## 1. Windows Defender registry change

File: [win_defender_realtime_tampering.yml](../rules/win_defender_realtime_tampering.yml)

- The rule uses the Windows registry set log source and Event ID 13.
- The evidence screenshot shows `sample4.exe` writing the `DisableRealtimeMonitoring` value as `1` under the Windows Defender Real-Time Protection key.
- The Sigma rule builder screenshot shows the key, value name, value, and ATT&CK mapping.
- The screenshots do not show the raw Sysmon Event ID 13 fields.
- The exact `TargetObject` and `Details` values used by the YAML cannot be confirmed from the screenshots.

**Current status:** Screenshot review completed. The registry behavior is supported. YAML parsing, Sysmon field mapping, Sigma validation, and event matching have not been demonstrated.

## 2. Periodic network beacon profile

File: [c2_periodic_beacon_network_profile.yml](../rules/c2_periodic_beacon_network_profile.yml)

- The egress log screenshot shows repeated records with timestamps, source, destination, port, and size.
- The records for `51.102.10.19:443` show 97-byte entries at 30-minute intervals.
- The Sigma rule builder screenshot shows remote IP set to Any, remote port set to Any, size set to 97 bytes, and frequency set to 1800 seconds.
- The YAML uses `PacketSize` and `BeaconIntervalSeconds`. These fields require a documented parser or field mapping and are not standard Sysmon Event ID 3 fields.
- The destination port restriction was removed from the YAML draft so it no longer conflicts with the Any setting shown in the rule builder.

**Current status:** Screenshot review completed. The repeated pattern and rule-builder settings are visible. YAML parsing, field mapping, Sigma validation, and interval logic have not been demonstrated.

## 3. File staging activity

File: [lotl_cmd_temp_data_staging.yml](../rules/lotl_cmd_temp_data_staging.yml)

- The process and file activity screenshot shows `sample6.exe` spawning child `cmd.exe` processes.
- It shows PID 2312 creating `%temp%\\exfiltr8.log`.
- The original rule used Sysmon Event ID 2. Event ID 2 records a file creation time change, not general file creation.
- The draft now uses Sysmon Event ID 11, the file creation event, and checks the creating process image and target filename.
- The screenshot supports the behavior, but it does not expose the raw Sysmon Event ID 11 fields.
- The rule does not correlate the file event with the parent process `sample6.exe`.

**Current status:** Screenshot review completed. The event choice has been corrected in the draft for file creation. YAML parsing, field matching, and process lineage correlation have not been demonstrated.

## Validation limits

The screenshots are the complete evidence set available for this lab project. They show the activity and rule configurations used in the cases. They do not provide raw Sysmon XML or JSON records, parser output, backend conversion results, or event-level test results.

A screenshot-supported review can document what happened in the simulated lab and explain why a detection rule was drafted. It cannot establish that a rule parses, converts, or matches events. Keep those distinctions clear when presenting the project.
