# Lab Indicators and Host Artifacts

This file collects the indicators and host artifacts explicitly recorded in the Summit lab notes. They belong to a simulated exercise and must not be treated as live threat intelligence.

## File hashes

| Case | File | Recorded value | Note |
| --- | --- | --- | --- |
| 1 | `sample1.exe` | `9c550591a25c6228....7180144859cc09efca8c` | The source note shows an abbreviated value. The complete SHA-256 value is not available in the recorded text. |
| 2 | `sample2.exe` | `d576245e85e6b752b2fdf....b0169fd04924d6cebc1cdf9` | The source note shows an abbreviated value. The complete hash is not available in the recorded text. |

## Network indicators

| Case | Type | Recorded value | Context |
| --- | --- | --- | --- |
| 2 | IP address | `154.35.10.113` | Outbound connection from `sample2.exe`, noted on port `4444` |
| 3 | Domain | `emudyn.bresonicz.info` | DNS lookup associated with `sample3.exe` |
| 3 | IP address | `62.123.140.9` | Resolution recorded for `emudyn.bresonicz.info` |
| 4 | Domain | `cranes0ft.iniware.xyz` | DNS resolution recorded during the `sample4.exe` activity |
| 5 | IP address | `51.102.10.19` | Egress beacon destination, noted on port `443` |
| 5 | Domain | `bababa10la.cn` | Domain associated with `beacon.bat` HTTP POST check-ins |

## Host artifacts and behavior

| Case | Artifact | Recorded detail |
| --- | --- | --- |
| 4 | Registry value | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection\DisableRealtimeMonitoring` set to `1` |
| 5 | Beacon pattern | 97-byte transmissions at 1800-second intervals, as described in the lab egress log |
| 6 | Process activity | `sample6.exe` spawning `cmd.exe` child processes |
| 6 | Staged file | `%temp%\exfiltr8.log` |

## Scope and limitations

- Values are transcribed from the existing Notion lab notes.
- The two hash values are abbreviated in the source and are not complete hashes.
- The file records what the simulation notes describe. It does not independently validate the indicators or prove that a rule matched raw event data.
