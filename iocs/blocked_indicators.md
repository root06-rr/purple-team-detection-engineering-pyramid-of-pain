# Extracted Indicators of Compromise (IOCs) & Containment Actions

This document catalogs all static, network, and host indicators extracted during the six-cycle purple-team threat emulation against simulated threat actor **"Sphinx"**.

## 1. Cryptographic File Hashes (Tier 1: Hash Values)
| Sample Name | SHA-256 Hash | Classification | Action Enforced |
| :--- | :--- | :--- | :--- |
| `sample1.exe` | `9c550591a25c6228cb7d74d970d133d75c961ffed2ef7180144859cc09efca8c` | `Trojan.Metasploit.A` (`application/x-dosexec`) | Added to global EDR IOC Blocklist |
| `sample2.exe` | `d576245e85e6b752b2fdf...b0169fd04924d6cebc1cdf9` | Recompiled Metasploit Variant | Superseded by Perimeter IP Block |

## 2. Network Infrastructure (Tier 2: IP Addresses)
| IP Address | Port / Protocol | Hosting ASN / Infrastructure | Associated Sample | Action Enforced |
| :--- | :--- | :--- | :--- | :--- |
| `154.35.10.113` | `TCP/4444` (HTTP GET) | Intrabuzz Hosting Limited | `sample2.exe` (`PID: 1927`) | Perimeter Firewall Egress `Deny` |
| `62.123.140.9` | `TCP/80, 1337` (HTTP GET) | Xplorita Cloud Services | `sample3.exe` (`PID: 1021`) | Neutralized via DNS Sinkhole |
| `102.23.20.118` | `TCP/80, 1337` (HTTP GET) | Xplorita Cloud Services | `sample4.exe` (`PID: 3806`) | Contained via Registry Sigma Rule |
| `51.102.10.19` | `TCP/443, 1382` (HTTP POST) | External C2 Listener | `sample5.exe` / `beacon.bat` | Contained via Beacon Sigma Rule |

## 3. Malicious Domains (Tier 3: Domain Names)
| Domain Name | Resolved IP | Purpose | Action Enforced |
| :--- | :--- | :--- | :--- |
| `emudyn.bresonicz.info` | `62.123.140.9` | Dynamic C2 & `backdoor.exe` staging | DNS Rule Manager Sinkhole (`Deny` + Subdomains) |
| `cranes0ft.iniware.xyz` | `102.23.20.118` | Secondary `backdoor.exe` payload retrieval | Contained at Host Artifact Layer |
| `bababa10la.cn` | `51.102.10.19` | Keep-alive C2 polling (`/keep-alive?hostname=WK102`) | Contained via Network Behavior Sigma Rule |

## 4. Host & Behavioral Artifacts (Tiers 4–6)
* **Registry Persistence / Defense Evasion:** `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection` -> `DisableRealtimeMonitoring = 1`
* **Staged Payloads & Scripts:** `backdoor.exe`, `beacon.bat` (97-byte POST payload every 1800 seconds)
* **Living-off-the-Land Staging Artifact:** `sample6.exe` (`PID: 8374`) spawning child `cmd.exe` shells (`PIDs: 3992, 1432, 2312`) writing `%AppData%\Local\Temp\exfiltr8.log`
