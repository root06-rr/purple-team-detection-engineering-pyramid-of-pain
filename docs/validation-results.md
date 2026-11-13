# Detection rule validation results

## Scope

I reviewed the three YAML rule drafts against the existing Notion lab notes and the screenshots stored in this repository. The screenshots are the complete evidence set available for this project.

The screenshots show:

- Registry activity for `sample4.exe`
- The registry rule builder configuration
- Repeated 97-byte network connections at 30-minute intervals
- The network rule builder configuration
- Process activity involving `sample6.exe` and `cmd.exe`
- File activity involving `%temp%\\exfiltr8.log`

These screenshots support an evidence-based review of the lab behavior and the intended detection logic. They are not raw Sysmon event exports, so they cannot confirm every event field or prove that the YAML rules matched events.

## Checks completed

| Check | Result | Meaning |
| --- | --- | --- |
| Screenshot review | Completed | The supplied screenshots were reviewed as the project's complete evidence set |
| Registry evidence comparison | Completed with limits | The registry key, value name, and value are visible |
| Beacon evidence comparison | Completed with limits | Repeated 97-byte connections at 30-minute intervals are visible |
| File staging evidence comparison | Completed with limits | The process and file activity screenshot shows cmd.exe creating exfiltr8.log |
| YAML parsing | Not run | No parser result is available |
| Sigma specification validation | Not run | Sigma tooling was not run |
| Backend conversion | Not run | No target SIEM or backend conversion was performed |
| Positive event testing | Not demonstrated | The screenshots do not show rule matching against raw event records |
| Negative event testing | Not demonstrated | No benign comparison test is shown |

## Rule-by-rule result

### Windows Defender registry rule

The screenshot shows `sample4.exe` writing the `DisableRealtimeMonitoring` value as `1` under the Windows Defender Real-Time Protection key. The rule builder screenshot also shows the intended registry condition.

The screenshots do not expose the raw Sysmon Event ID 13 fields. The exact `TargetObject` and `Details` values in the YAML therefore remain unconfirmed.

**Result:** The intended registry behavior is supported by the screenshots. The YAML field mapping and event matching are not validated.

### Periodic network beacon rule

The network log screenshot shows repeated 97-byte connections to `51.102.10.19:443` at 30-minute intervals. The rule builder screenshot shows remote IP set to Any, remote port set to Any, size set to 97 bytes, and frequency set to 1800 seconds.

The YAML uses `PacketSize` and `BeaconIntervalSeconds`. These fields require a documented parser or field mapping and are not standard Sysmon Event ID 3 fields. The destination port restriction was removed from the YAML draft to match the Any setting shown in the rule builder.

**Result:** The repeated network pattern and intended rule-builder settings are supported by the screenshots. The YAML field mapping and interval logic are not validated.

### File staging rule

The process and file activity screenshot shows `sample6.exe` spawning `cmd.exe`, with a child process creating `%temp%\\exfiltr8.log`. The original Event ID 2 selection did not match the stated file creation behavior. The revised draft uses Event ID 11 and checks `Image` and `TargetFilename`.

The screenshot supports the behavior, but it does not expose the raw Sysmon Event ID 11 fields or prove that the rule matched an event.

**Result:** The event choice in the draft has been corrected for file creation. Field matching and process lineage correlation are not validated.

## Final assessment

The screenshots provide the project's available evidence for the six simulated cases and support the behavior described in the case notes. They are suitable for documenting the lab work.

The three YAML files remain detection rule drafts. YAML parsing, Sigma validation, backend conversion, and event-level testing have not been demonstrated. Do not describe the rules as fully validated or production-ready.
