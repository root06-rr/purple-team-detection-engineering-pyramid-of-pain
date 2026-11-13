# Detection rule validation results

## Scope

I reviewed the three YAML rule files against the existing Notion lab notes and the evidence screenshots stored in this repository.

The available material includes:

- Registry activity for `sample4.exe`
- A registry rule builder screen
- A text-style egress log showing repeated 97-byte connections
- A network rule builder screen
- Process lineage and file activity for `sample6.exe`
- The original YAML rule drafts

The available material does not include raw Sysmon event records or the original network log file.

## Checks completed

| Check | Result | Meaning |
| --- | --- | --- |
| YAML parsing | Passed for all three revised files | The files can be read as YAML |
| Registry evidence comparison | Partially supported | The registry key, value name, and value are visible in the screenshot |
| Beacon evidence comparison | Partially supported | Repeated 97-byte connections at 30-minute intervals are visible in the log screenshot |
| File staging evidence comparison | Partially supported | The process and file activity screenshot shows cmd.exe creating exfiltr8.log |
| Sigma specification validation | Not run | Sigma tooling was not available in the current environment |
| Backend conversion | Not run | No target SIEM or backend was specified |
| Positive event testing | Not run | Raw event records are not present |
| Negative event testing | Not run | Benign comparison events are not present |

## Rule-by-rule result

### Windows Defender registry rule

The screenshot supports the intended behavior. It shows `sample4.exe` writing the `DisableRealtimeMonitoring` value as `1`. It does not show the raw Sysmon Event ID 13 fields. The exact `TargetObject` and `Details` values remain unconfirmed.

**Result:** Evidence-aligned draft. Not event-tested.

### Periodic network beacon rule

The log screenshot shows repeated 97-byte connections to `51.102.10.19:443` at 30-minute intervals. The YAML uses `PacketSize` and `BeaconIntervalSeconds`, which require a custom parser or field mapping. The rule builder screenshot also shows the remote port as Any, while the YAML restricts it to port 443.

**Result:** Pattern visible in the supplied evidence. Field mapping and Sigma logic remain unvalidated.

### File staging rule

The process and file activity screenshot shows `sample6.exe` spawning `cmd.exe`, with a child process creating `%temp%\\exfiltr8.log`. The original Event ID 2 selection did not match the stated file creation behavior. The revised draft uses Event ID 11 and checks `Image` and `TargetFilename`.

**Result:** Event choice corrected in the draft. Raw event matching remains untested.

## Final assessment

The three revised files passed YAML parsing. This is a syntax check, not a Sigma validation or detection test.

The registry and file rules need raw Sysmon events before their field mappings can be confirmed. The network rule needs a documented mapping from the egress log fields to the rule fields, plus a clear definition of how the 1800-second interval is evaluated.

No rule should currently be described as fully validated or production-ready.
