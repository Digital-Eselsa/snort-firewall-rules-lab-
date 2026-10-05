# Command Reference

> Use this file as a working command checklist. Record your actual output in the lab notes and screenshots.

## 1. Configure DHCP

```bash
sudo ./lab.support.files/scripts/configure_as_dhcp.sh
```

## 2. Verify Network Configuration

```bash
ifconfig
```

## 3. Test Internet Connectivity

```bash
ping www.cisco.com
```

Stop the ping with:

```text
Ctrl+C
```

## 4. Start Mininet

```bash
sudo ./lab.support.files/scripts/cyberops_extended_topo_no_fw.py
```

Expected prompt:

```text
mininet>
```

## 5. Open R1

```text
xterm R1
```

## 6. Start Snort

From the R1 shell:

```bash
./lab.support.files/scripts/start_snort.sh
```

## 7. Open Snort Alert Monitor

In another R1 terminal:

```bash
tail -f /var/log/snort/alert
```

## 8. Open H5 and H10

From the Mininet prompt:

```text
xterm H5
xterm H10
```

## 9. Start the Simulated Server

On H10:

```bash
./lab.support.files/scripts/mal_server_start.sh
```

## 10. Verify the Web Server

```bash
netstat -tunpa
```

The source lab expects the simulated web service to listen on TCP port `6666`.

## 11. Generate the Download

On H5:

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

## 12. Start Packet Capture

On H5:

```bash
tcpdump -i H5-eth0 -w nimda.download.pcap &
```

## 13. Stop Packet Capture

Bring the background process forward:

```bash
fg
```

Then:

```text
Ctrl+C
```

## 14. Verify PCAP

```bash
ls -l
```

Confirm that:

```text
nimda.download.pcap
```

exists and has a non-zero size.

## 15. Inspect Firewall Rules

On R1:

```bash
iptables -L -v
```

## 16. Add the Blocking Rule

Use the rule specified by the source lab:

```bash
iptables -I FORWARD -p tcp -d 209.165.202.133 --dport 6666 -j DROP
```

## 17. Verify the Rule

```bash
iptables -L -v
```

Look for the DROP rule in the `FORWARD` chain.

## 18. Test the Firewall

On H5:

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

Document the resulting connection failure/timeout.

## 19. Exit Mininet

At the main Mininet prompt:

```text
quit
```

## 20. Clean Up Mininet

```bash
sudo mn -c
```
