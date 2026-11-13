# Detection rule review

This page records technical checks needed before the YAML files are described as tested or ready for operational use. The rules are retained as lab artifacts. The validation status is based on the files and evidence currently in the repository.

## 1. Windows Defender registry change

File: [win_defender_realtime_tampering.yml](../rules/win_defender_realtime_tampering.yml)

- The rule uses the Windows registry set log source and Event ID 13.
- The evidence screenshot shows `sample4.exe` writing the `DisableRealtimeMonitoring` value as `1` under the Windows Defender Real-Time Protection key.
- The Sigma rule builder screenshot shows the key, value name, value, and ATT&CK mapping.
- The screenshots do not show the raw Sysmon Event ID 13 fields.
- Confirm the exact `TargetObject` and `Details` values against the raw event. The current rule uses `DWORD (0x00000001)` for `Details`, which is not confirmed by the screenshot.
- Confirm that the rule parses with the Sigma tooling used for the project.

**Current status:** YAML syntax checked. Evidence supports the registry behavior. Sysmon field mapping and detection matching are not validated.

## 2. Periodic network beacon profile

File: [c2_periodic_beacon_network_profile.yml](../rules/c2_periodic_beacon_network_profile.yml)

- The egress log screenshot shows repeated records with timestamps, source, destination, port, and size.
- The records for `51.102.10.19:443` show 97-byte entries at 30-minute intervals.
- The Sigma rule builder screenshot shows remote IP set to Any, remote port set to Any, size set to 97 bytes, and frequency set to 1800 seconds.
- The YAML rule includes `PacketSize` and `BeaconIntervalSeconds`. These are not standard Sysmon Event ID 3 fields.
- The evidence does not document a parser or field mapping from the text log to those YAML fields.
- The YAML rule also limits the destination port to 443, while the rule builder screenshot shows Any. Confirm whether the port restriction was intended.

**Current status:** YAML syntax checked. The repeated pattern is visible in the supplied log screenshot. The Sigma field mapping and interval logic are not validated.

## 3. File staging activity

File: [lotl_cmd_temp_data_staging.yml](../rules/lotl_cmd_temp_data_staging.yml)

- The process and file activity screenshot shows `sample6.exe` spawning child `cmd.exe` processes.
- It shows PID 2312 creating `%temp%\\exfiltr8.log`.
- The original rule used Sysmon Event ID 2. Event ID 2 records a file creation time change, not general file creation.
- The draft now uses Sysmon Event ID 11, the file creation event, and checks the creating process image and target filename.
- The evidence is a sandbox summary rather than a raw Sysmon Event ID 11 record.
- The rule does not correlate the file event with the parent process `sample6.exe`. That relationship is described in the notes but cannot be validated from the available raw data because no raw events are included.

**Current status:** YAML syntax checked. The event type has been corrected for file creation. Field matching and process lineage correlation are not validated.

## Validation limits

The repository contains screenshots and a text-style network log image. It does not contain raw Sysmon XML or JSON events, the original `outgoing_connections.log` file, Sigma parser output, or positive and negative test results.

A YAML parser check confirms only that the files are valid YAML. It does not confirm that a rule follows the Sigma specification, that a backend can convert it, or that it matches real event data.

Do not describe these rules as tested or validated detections until those checks have been performed.
