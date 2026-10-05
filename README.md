# Snort and Firewall Rules Lab

> **Cybersecurity Lab Documentation — IDS Alert Detection, Packet Capture, and Firewall Rule Tuning**

## Lab Overview

This repository documents the Cisco CyberOps **Lab - Snort and Firewall Rules** activity.

The lab focuses on:

- Preparing the CyberOps Workstation virtual environment
- Starting a Mininet topology
- Running Snort in IDS mode
- Monitoring Snort alerts in real time
- Simulating a malicious web server
- Capturing the network transaction with `tcpdump`
- Analyzing the purpose of the resulting PCAP
- Inspecting `iptables` chains and rules
- Adding a firewall rule to block traffic to the identified server
- Verifying that the firewall blocks the connection
- Terminating and cleaning up the Mininet environment

The source lab identifies the required resource as a **CyberOps Workstation virtual machine** with an Internet connection.

## Repository Structure

```text
snort-firewall-rules-lab/
├── README.md
├── COMMANDS.md
├── EVIDENCE_CHECKLIST.md
├── .gitignore
├── LICENSE
├── screenshots/
│   ├── 01-environment/
│   ├── 02-snort-ids/
│   ├── 03-pcap-capture/
│   ├── 04-iptables-firewall/
│   └── 05-verification/
├── evidence/
│   ├── pcap/
│   └── logs/
├── commands/
├── docs/
└── scripts/
```

## Lab Objectives

1. Prepare the virtual environment.
2. Configure network connectivity.
3. Start the Mininet topology.
4. Start Snort as an IDS.
5. Monitor `/var/log/snort/alert`.
6. Generate a test download from H5 to the simulated server on H10.
7. Observe the Snort alert.
8. Capture the transaction with `tcpdump`.
9. Inspect the `iptables` configuration.
10. Add a `FORWARD` rule that drops TCP traffic to the identified server and port.
11. Verify that the connection is blocked.
12. Terminate and clean up Mininet.

## Environment

| Component | Role |
|---|---|
| CyberOps Workstation | Main lab VM / Mininet environment |
| R1 | Router/firewall and Snort IDS host |
| H5 | Client generating the HTTP request |
| H10 | Simulated malicious web server |
| Snort | Intrusion Detection System |
| iptables | Linux firewall |
| tcpdump | Packet capture utility |
| Mininet | Virtual network environment |

## Key Security Concepts

### IDS vs Firewall

The lab explains that firewalls commonly compare packet headers against rules, while IDS systems can inspect packet payloads against signatures.

Both use:

- **Matching components** — characteristics of traffic being inspected.
- **Action components** — what should happen after a match.

### Snort Alert

During the lab, Snort is expected to detect traffic associated with the simulated malicious server and generate an alert.

Document your **actual alert output** in:

```text
screenshots/02-snort-ids/
evidence/logs/
```

### Packet Capture

The lab uses `tcpdump` to create:

```text
nimda.download.pcap
```

Place your actual capture in:

```text
evidence/pcap/
```

Do **not** fabricate packet captures. Only commit a PCAP generated during your own lab.

### Firewall Rule

The lab adds a rule to the `FORWARD` chain to drop TCP traffic destined for the identified server on TCP port `6666`.

Document your actual `iptables -L -v` output in:

```text
screenshots/04-iptables-firewall/
```

## Questions and Findings

Record your answers and observations in:

**[LAB_NOTES.md](docs/LAB_NOTES.md)**

Suggested evidence for each major finding:

- Terminal showing IP configuration
- Successful connectivity test
- Mininet startup
- R1 shell
- Snort startup
- Real-time Snort alert
- H10 web service listening on TCP 6666
- Successful download before firewall rule
- `tcpdump` capture running
- PCAP file saved with non-zero size
- Initial `iptables -L -v`
- Added `FORWARD` DROP rule
- Failed/timed-out download after the firewall rule
- Mininet cleanup

## Evidence Policy

This repository intentionally contains **placeholders rather than fabricated evidence**.

Replace placeholder files with your own:

- screenshots
- terminal output
- Snort alerts
- PCAP
- notes

Avoid uploading unrelated credentials, passwords, tokens, private keys, or sensitive personal information.

## Completion Checklist

- [ ] Environment prepared
- [ ] DHCP configuration completed
- [ ] IP address verified
- [ ] Internet connectivity tested
- [ ] Mininet started
- [ ] R1 shell opened
- [ ] Snort started
- [ ] Snort alert monitoring started
- [ ] H10 service verified
- [ ] Download completed before firewall rule
- [ ] Snort alert documented
- [ ] PCAP captured
- [ ] PCAP file verified
- [ ] Initial iptables rules documented
- [ ] FORWARD DROP rule added
- [ ] Rule verified with `iptables -L -v`
- [ ] Download blocked after firewall rule
- [ ] Mininet terminated
- [ ] Mininet cleanup completed
- [ ] Screenshots organized
- [ ] README updated with findings
- [ ] Repository pushed to GitHub
