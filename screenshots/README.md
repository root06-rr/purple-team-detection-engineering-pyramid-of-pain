# Evidence Screenshots Directory

To complete the visual walkthrough in `README.md`, export your 11 evidence screenshots from your Notion page (`1. Summit: Detection Engineering & Pyramid of Pain`) and place them in this folder using the naming convention below:

1. `01_pyramid_of_pain_overview.png` — Engagement timeline overview
2. `02_case1_sandbox_triage.png` — `sample1.exe` Malware Sandbox Metasploit tags & SHA-256 hash
3. `03_case1_edr_hash_block.png` — EDR IOC Management SHA-256 blocklist rule
4. `04_case2_network_telemetry.png` — `sample2.exe` outbound HTTP GET to `154.35.10.113:4444`
5. `05_case2_firewall_egress_deny.png` — Perimeter firewall egress Deny rule
6. `06_case3_dns_lookup_staging.png` — `sample3.exe` DNS lookup for `emudyn.bresonicz.info`
7. `07_case3_dns_sinkhole_rule.png` — DNS Rule Manager sinkhole policy
8. `08_case4_registry_tampering.png` — `sample4.exe` modifying `DisableRealtimeMonitoring = 1`
9. `09_case4_sigma_registry_rule.png` — Sysmon Sigma rule blocking Defender registry tampering
10. `10_case5_c2_beacon_logs.png` — 97-byte / 1800-second egress C2 heartbeat telemetry & Sigma rule
11. `11_case6_ttp_exfil_sigma.png` — `sample6.exe` spawning `cmd.exe` to stage `%temp%\exfiltr8.log` & Sigma rule
