# Purple-Team Detection Engineering Lab

A simulated purple-team lab based on David Bianco's Pyramid of Pain. The project follows six threat-emulation cases and records how the defensive response moves from static indicators toward host and behavior-based detection.

This repository is a portfolio record of the lab work and the detection concepts documented in my notes. It is not a production deployment or a claim of professional incident-response experience.

## Project at a glance

- **Environment:** Simulated Windows enterprise workstation and local virtual lab
- **Threat profile:** Sphinx, a simulated threat actor
- **Method:** David Bianco's Pyramid of Pain
- **Framework:** MITRE ATT&CK references included in the original notes and rule files
- **Cases:** Hash values, IP addresses, domain names, host artifacts, tools, and TTPs
- **Detection artifacts:** Three YAML Sigma-style rule drafts
- **Indicators:** Recorded within the relevant case notes where available

## How the project is organized

| Location | What is there |
| --- | --- |
| [cases/](cases/) | The six lab cases, organized by Pyramid of Pain tier |
| [rules/](rules/) | Three YAML detection rule drafts from the lab |
| [evidence/](evidence/) | Existing evidence files from the original lab write-up |
| [docs/rule-review.md](docs/rule-review.md) | Technical review notes and validation limits |
| [docs/validation-results.md](docs/validation-results.md) | Checks completed against the existing evidence |

## The six cases

| Case | Pyramid tier | Main activity | Defensive focus |
| --- | --- | --- | --- |
| [01. Hash values](cases/01-hash-values.md) | Hash Values | Triage of sample1.exe | Record a file hash and add it to the EDR blocklist |
| [02. IP addresses](cases/02-ip-addresses.md) | IP Addresses | Review of sample2.exe network activity | Record the destination IP and document a firewall deny rule |
| [03. Domain names](cases/03-domain-names.md) | Domain Names | Review of sample3.exe DNS activity | Document a DNS sinkhole rule |
| [04. Host artifacts](cases/04-host-artifacts.md) | Host Artifacts | Review of Windows Defender registry changes | Create a registry-focused Sigma rule |
| [05. Tools and beaconing](cases/05-tools-and-beaconing.md) | Tools | Review of repeated outbound connections | Draft a network behavior Sigma rule |
| [06. TTPs and file staging](cases/06-ttps-and-file-staging.md) | TTPs | Review of cmd.exe process activity and a staged file | Draft a file activity Sigma rule |

## How I approached the lab

I followed the six cases in order. In each case, I recorded the activity described in the lab notes, identified the relevant indicator or behavior, and documented the defensive response. The first three cases focus on indicators that can change when an attacker modifies a file or infrastructure. The last three move toward host artifacts, tool behavior, and a living-off-the-land technique.

The case pages separate the observed lab activity, the response recorded in the notes, and the related repository artifact. They do not treat a written response as proof that a detection rule was successfully tested.

## Detection rule status

The three YAML files are retained as lab artifacts. YAML parsing has not been run, and the rules have not been validated with a Sigma parser or tested against raw event records.

- The registry evidence shows the process, registry key, value name, and value. It does not include the raw Sysmon Event ID 13 record needed to confirm the exact field mapping.
- The beacon evidence is a text-based egress log with timestamps, source, destination, port, and size. The current rule uses custom fields that need a documented mapping. Sysmon Event ID 3 does not provide the packet size and interval fields used by the rule.
- The file staging rule uses Sysmon Event ID 11 for file creation. The evidence shows cmd.exe creating the file, but it does not include the raw Sysmon event needed to test the rule.

See [the rule review](docs/rule-review.md) and [validation results](docs/validation-results.md) before treating any rule as operational or validated.

## What this project demonstrates

- Working through a simulated threat-emulation sequence
- Organizing file, network, domain, registry, and file activity indicators within the case notes
- Relating defensive responses to the Pyramid of Pain
- Writing YAML-based Sigma-style detection logic
- Recording MITRE ATT&CK references from the lab material
- Reviewing the limits of detection logic before claiming it is ready for use

## Project status

This repository contains the case notes, rule drafts, and evidence files from the lab. It does not currently include raw Sysmon event fixtures, a repeatable test harness, Sigma parser output, or documented rule match results. For that reason, I describe the YAML files as detection rule drafts that need further validation.

All activity described here is simulated lab work. Indicators and hostnames are retained as lab artifacts and should not be treated as live threat intelligence.

## Original Lab Notes

This project is based on my original lab notes and observations documented in Notion.

[View Original Lab Notes](https://app.notion.com/p/1-Summit-Detection-Engineering-Pyramid-of-Pain-3eaf055fceba8015b3d8d1dbf21f4892?source=copy_link)

The GitHub repository contains the organized case studies, available evidence screenshots, and detection rule drafts developed from those notes.
