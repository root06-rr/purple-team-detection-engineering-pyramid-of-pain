# Detection rule review

This page records technical checks needed before the YAML files are described as tested or ready for operational use. The rules are retained as artifacts from the lab. This review does not claim that they have been validated.

## 1. Windows Defender registry change

File: [win_defender_realtime_tampering.yml](../rules/win_defender_realtime_tampering.yml)

- The rule uses the Windows registry set log source and Event ID 13.
- The target registry path matches the setting described in the lab notes.
- Confirm the exact field names and value representation against the registry event produced by the lab source.
- Confirm that the rule parses with the Sigma tooling used for the project.

## 2. Periodic network beacon profile

File: [c2_periodic_beacon_network_profile.yml](../rules/c2_periodic_beacon_network_profile.yml)

- The rule uses the Windows network connection log source and Event ID 3.
- The rule includes `PacketSize` and `BeaconIntervalSeconds`.
- These are not standard fields in Sysmon Event ID 3.
- The lab notes describe a 97-byte payload and a 1800-second interval, but the repository does not document a standard Sysmon field mapping for those values.
- Confirm the actual data source and its schema. Until then, the rule is a draft and should not be presented as a portable Sysmon detection.

## 3. File staging activity

File: [lotl_cmd_temp_data_staging.yml](../rules/lotl_cmd_temp_data_staging.yml)

- The rule uses Sysmon Event ID 2.
- Sysmon Event ID 2 records a file creation time change. It is not the general file creation event.
- The rule description refers to file creation or modification, so the event choice does not currently support the wording.
- Confirm which event was present in the lab evidence and align the rule selection with that event's documented fields.
- The current rule does not include process lineage fields, even though the case notes describe a child `cmd.exe` process.

## Validation status

The repository currently contains three YAML rule files and supporting lab notes. It does not contain a repeatable test harness, sample event fixtures, parser output, or documented match results. The rules should therefore be described as drafts that need validation.

## Suggested validation record

When the original lab data is available, record the following for each rule:

1. The source product and event type.
2. The exact event fields used by the rule.
3. Whether the YAML parses successfully.
4. The event used to test a positive match.
5. A benign event used to check for false positives.
6. The actual result of each test.

Do not fill in these results until the tests have been performed.
