# Case 05: Tools and beaconing

**Pyramid tier:** Tools  
**Sample:** `sample5.exe` and `beacon.bat`  
**Defensive focus:** Repeated outbound network activity

## Lab activity

The notes describe repeated outbound connections in a 12-hour egress log. The recorded pattern was traffic to `51.102.10.19:443` with a 97-byte payload at 1800-second intervals. The notes also describe `beacon.bat` sending repeated HTTP POST requests to the `/keep-alive` endpoint on `bababa10la.cn`.

## Indicators and behavior recorded

- Destination: `51.102.10.19`
- Port: `443`
- Payload size recorded in the notes: 97 bytes
- Interval recorded in the notes: 1800 seconds
- Domain: `bababa10la.cn`
- Script: `beacon.bat`

## Defensive response recorded in the notes

A network behavior Sigma rule was authored and is stored at [c2_periodic_beacon_network_profile.yml](../rules/c2_periodic_beacon_network_profile.yml).

The current rule includes `PacketSize` and `BeaconIntervalSeconds`. These fields are not standard Sysmon Event ID 3 fields. The rule is a draft until the event source and field mapping are confirmed.

## MITRE ATT&CK reference

The original notes map the activity to Command and Control, technique `T1071.001`.

## Related files

- [Network rule](../rules/c2_periodic_beacon_network_profile.yml)
- [Indicator record](../iocs/blocked_indicators.md)
- [Evidence files](../evidence/)

## What this case shows

This case records a move from blocking a fixed network indicator toward identifying repeated communication behavior. The current YAML file does not prove that the timing pattern can be detected from standard Sysmon Event ID 3 data.
