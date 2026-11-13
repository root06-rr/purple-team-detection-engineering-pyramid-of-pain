# Case 02: IP addresses

**Pyramid tier:** IP Addresses  
**Sample:** `sample2.exe`  
**Defensive focus:** Network telemetry and egress filtering

## Lab activity

The notes describe a modified version of the sample with a changed file hash. Sandbox network activity showed a direct outbound HTTP GET request to `154.35.10.113` over TCP port `4444`. The notes record no DNS lookup for this connection.

## Indicator recorded

- Destination IP: `154.35.10.113`
- Port: `4444`
- Protocol: HTTP over TCP, as described in the notes
- Associated sample: `sample2.exe`

The replacement sample hash in the original notes is abbreviated. It is not a complete SHA-256 value and should not be used as a blocklist indicator.

## Defensive response recorded in the notes

An outbound deny rule was configured on the simulated perimeter firewall for traffic to the destination IP.

## Related files

- [Indicator record](../iocs/blocked_indicators.md)
- [Evidence files](../evidence/)

## What this case shows

A hash block applies to a specific file. An IP-based control moves the response to the network destination, although an attacker can change infrastructure.
