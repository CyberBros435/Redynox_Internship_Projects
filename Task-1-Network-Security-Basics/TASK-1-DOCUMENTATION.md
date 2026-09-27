# Task 1 — Introduction to Network Security Basics
**Redynox Cybersecurity Internship**

## 1. Network Threats Researched

**Virus** — Malicious program that attaches to files/programs, spreads when the infected file is executed.

**Worm** — Spreads automatically across networks, no user action needed.

**Trojan** — Disguises as legitimate software, executes harmful actions once run.

**Phishing** — Social engineering attack tricking users into revealing sensitive info via fake messages/links/sites.

## 2. Security Concepts Understood

- **Firewall** — Controls traffic between networks, blocks unauthorized connections.
- **Encryption** — Converts readable data into protected form, unreadable without a key.
- **Secure Network Config** — Strong passwords, changed default credentials, WPA2/WPA3 enabled, minimal open access.

## 3. Security Measures Implemented

- **Windows Defender Firewall enabled** on all three profiles (Domain, Private, Public) — confirmed via Overview panel. See `Screenshots/firewall-overview-enabled.png`
- **Inbound connections blocked by default** unless a rule allows them — confirmed on all profiles. See `Screenshots/firewall-inbound-rules.png`
- **Outbound connections allowed by default**, reviewed the full outbound rule list to check for unexpected allowed programs. See `Screenshots/firewall-outbound-rules.png`
- **Custom test block rule created** ("test", Inbound, Block, All profiles) to verify rule creation works correctly. See `Screenshots/firewall-custom-rule-test.png`

## 4. Network Traffic Monitoring

Captured TCP traffic using an online packet viewer (no local Wireshark install used).

- **Protocol observed**: TCP three-way handshake and teardown pattern visible — SYN, SYN/ACK, ACK, and FIN/ACK sequences between hosts 192.168.200.21 and 192.168.200.135. See `Screenshots/network-traffic-tcp.png`
- **What this shows**: normal TCP session setup (SYN→SYN,ACK→ACK) and graceful close (FIN,ACK exchanged both directions) on ports 2000/6711/6712.
- **Suspicious traffic**: none flagged in this sample — traffic follows a standard, well-formed TCP handshake/teardown with no unusual ports, repeated connection floods, or cleartext credential patterns.

> **Gap to close**: this only proves TCP-level review, not HTTP/DNS traffic identification as the task guideline explicitly asks for. Recommend pulling `http.cap` from Wireshark's official sample captures (wiki.wireshark.org/SampleCaptures) into the same viewer and adding one HTTP + one DNS screenshot before final submission.

## 5. Why These Measures Protect the Network

The firewall blocks unsolicited inbound connections before they reach any device, cutting off the most common entry point for network threats. Reviewing outbound rules helps catch software silently phoning out. A custom block rule demonstrates the ability to actively respond to a specific threat/program, not just rely on defaults. Encryption (WPA2/WPA3, not shown here but standard practice) stops attackers on the same network from reading traffic in transit.

## 6. Reflection — Larger Network

For a bigger/enterprise network I'd add: network segmentation (VLANs), an IDS/IPS (e.g., Snort/Suricata), centralized logging (SIEM), and MFA on all admin access — a single firewall + strong passwords doesn't scale past a home lab.

## 7. Educating Others

I'd tell non-technical users: never reuse passwords across accounts, don't click links from unknown senders, keep router firmware updated, and always check for HTTPS before entering sensitive info — most breaches start from human error, not sophisticated hacking.
