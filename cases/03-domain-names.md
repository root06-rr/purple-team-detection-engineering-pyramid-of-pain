# Case 03: Domain names

**Pyramid tier:** Domain Names  
**Sample:** `sample3.exe`  
**Defensive focus:** DNS telemetry and sinkholing

## Lab activity

The notes describe a new sample that used a domain name instead of the previously recorded static IP. Sandbox network activity showed a DNS query for `emudyn.bresonicz.info`, resolving to `62.123.140.9`. The notes also record HTTP GET activity over ports `1337` and `80` and an attempted download of `backdoor.exe`.

## Indicators recorded

- Domain: `emudyn.bresonicz.info`
- Resolved IP: `62.123.140.9`
- Associated sample: `sample3.exe`
- Secondary file named in the notes: `backdoor.exe`

## Defensive response recorded in the notes

A DNS sinkhole or deny rule was configured for the domain and its subdomains in the simulated DNS rule manager.

## Related files

- [Indicator record](../iocs/blocked_indicators.md)
- [Evidence files](../evidence/)

## What this case shows

Domain-based controls can address infrastructure identified through DNS activity. They still depend on recognizing and maintaining the relevant domain indicators.
