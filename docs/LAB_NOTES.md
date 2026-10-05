# Lab Notes and Answers

## Student Information

- **Name:** 
- **Course / Program:** 
- **Institution / Training Center:** 
- **Date:** 
- **Lab:** Snort and Firewall Rules
- **Environment:** CyberOps Workstation / Mininet

---

# Part 1 — Preparing the Virtual Environment

## 1. Network Configuration

### Command

```bash
sudo ./lab.support.files/scripts/configure_as_dhcp.sh
```

### Observation

Record the result of the DHCP configuration:

> 

### Evidence

`screenshots/01-environment/`

---

## 2. IP Address Verification

### Command

```bash
ifconfig
```

### IP Address Observed

> 

### Evidence

`01-ip-config.png`

---

## 3. Connectivity Test

### Command

```bash
ping www.cisco.com
```

### Result

> 

### Evidence

`02-connectivity-test.png`

---

# Part 2 — Firewall and IDS Logs

## Step 1 — Real-Time IDS Log Monitoring

### 4. Mininet Startup

### Command

```bash
sudo ./lab.support.files/scripts/cyberops_extended_topo_no_fw.py
```

### Observation

> 

---

## 5. R1 Shell

### Question

What user is logged into the R1 shell? What is the indicator?

### Answer

> 

### Evidence

`screenshots/02-snort-ids/01-r1-shell.png`

---

## 6. Start Snort

### Command

```bash
./lab.support.files/scripts/start_snort.sh
```

### Observation

> 

### Evidence

`screenshots/02-snort-ids/02-snort-started.png`

---

## 7. Monitor Snort Alerts

### Command

```bash
tail -f /var/log/snort/alert
```

### Observation

> 

---

## 8. H10 Web Server

### Command

```bash
./lab.support.files/scripts/mal_server_start.sh
```

Then:

```bash
netstat -tunpa
```

### Listening Port

> 

### Evidence

`screenshots/02-snort-ids/`

---

## 9. Download Test

### Command

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

### Questions

**What port is used when communicating with the malware web server? What is the indicator?**

> 

**Was the file completely downloaded?**

> 

**Did the IDS generate any alerts related to the file download?**

> 

### Evidence

`screenshots/02-snort-ids/04-snort-alert.png`

---

## 10. Analyze the Snort Alert

Record your actual alert:

```text
Paste your actual Snort alert here.
```

### Source IPv4 Address

> 

### Destination IPv4 Address

> 

### Source Port

> 

### Destination Port

> 

### Timestamp

> 

### IDS Signature Message

> 

---

# Step 11 — Packet Capture

### Start Capture

```bash
tcpdump -i H5-eth0 -w nimda.download.pcap &
```

### Repeat Download

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

### Stop Capture

```bash
fg
```

Then press:

```text
Ctrl+C
```

### PCAP Filename

> 

### PCAP Size

> 

### Question

How can this PCAP file be useful to a security analyst?

### Answer

> 

### Evidence

- `screenshots/03-pcap-capture/`
- `evidence/pcap/nimda.download.pcap`

---

# Step 12 — Inspect Firewall Rules

### Command

```bash
iptables -L -v
```

### Question

What chains are currently in use by R1?

### Answer

> 

### Evidence

`screenshots/04-iptables-firewall/01-iptables-before.png`

---

# Step 13 — Add the Firewall Rule

### Command

```bash
iptables -I FORWARD -p tcp -d 209.165.202.133 --dport 6666 -j DROP
```

### Explain the Rule

| Component | Meaning |
|---|---|
| `-I FORWARD` | Inserts a rule into the FORWARD chain |
| `-p tcp` | Matches TCP traffic |
| `-d 209.165.202.133` | Matches the destination server |
| `--dport 6666` | Matches destination TCP port 6666 |
| `-j DROP` | Drops matching traffic |

---

# Step 14 — Verify the Firewall Rule

### Command

```bash
iptables -L -v
```

### Actual Result

```text
Paste relevant output here.
```

### Evidence

`screenshots/04-iptables-firewall/02-drop-rule-added.png`

---

# Step 15 — Test the Firewall

### Command

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

### Question

Was the download successful this time? Explain.

### Answer

> 

### Question

What would be a more aggressive but also valid approach when blocking the offending server?

### Answer

> 

### Evidence

`screenshots/05-verification/04-download-blocked.png`

---

# Part 3 — Terminate and Clear Mininet Process

## 16. Terminate Mininet

At the Mininet prompt:

```text
quit
```

### Observation

> 

## 17. Clean Up Mininet

```bash
sudo mn -c
```

### Observation

> 

### Evidence

`screenshots/05-verification/`

---

# Security Analysis

## What happened?

Summarize the attack/detection/blocking flow:

> 

## Detection

How did Snort identify the suspicious activity?

> 

## Network Traffic

What important source/destination information was visible in the alert?

> 

## Packet Capture

What additional investigation value does the PCAP provide?

> 

## Firewall Mitigation

How did the `FORWARD` DROP rule change the behavior?

> 

## SOC Analyst Takeaway

What would you investigate next in a real SOC environment?

> 

---

# Final Reflection

### 1. Most important concept learned

> 

### 2. Most useful command

> 

### 3. Most important evidence collected

> 

### 4. What I would improve in a future investigation

> 
