# Redynox Internship Projects

Cybersecurity Internship at **Redynox** — two hands-on tasks covering network security and web application security, done on a personal lab (Kali Linux VM + Windows host) with no paid tools.

**Intern:** Mudasir ([@CyberBros435](https://github.com/CyberBros435))

---

## Repository Structure

```
Redynox_Internship_Projects/
├── README.md
├── Task1_Network_Security/
│   ├── Task1_Network_Security_Report.docx
│   ├── Task1_Network_Security_Report.pdf
│   ├── LAB_STEPS.md
│   └── screenshots/
│       ├── 01_firewall_profiles.png
│       ├── 02_block_rule.png
│       ├── 03_router_security.png
│       ├── 04_dns.png
│       ├── 05_http.png
│       ├── 06_tls.png
│       └── 07_tcp_handshake.png
└── Task2_WebApp_Security/
    ├── Task2_WebApp_Security_Report.docx
    ├── README.md
    └── screenshots/
        ├── 01_burp_sitemap.png
        ├── 02_sqli_payload_login.png
        ├── 03_burp_http_history_login.png
        ├── 04_sqli_login_success.png
        ├── 05_xss_payload_search.png
        ├── 06_xss_alert.png
        └── 07_csrf_no_token_forms.png
```

---

## Task 1 — Network Security Basics

**Goal:** Understand common network threats and apply basic protections on a small network, then read and explain real traffic.

**Environment:** Home Tenda router + Windows host + Kali Linux VM (VirtualBox), used as the traffic-capture machine.

**What was done:**
- Researched 4 core threats — viruses, worms, trojans, phishing — how each works and how to defend against it
- Verified Windows Defender Firewall active on Domain, Private, and Public profiles
- Created and verified a custom outbound block rule (port 80) in Windows Defender Firewall with Advanced Security
- Set router Wi-Fi security to WPA/WPA2-PSK and changed the default Wi-Fi password
- Captured live traffic in Wireshark on the Kali VM's `eth0` interface and filtered it: `dns`, `http`, `tls`, `tcp` (three-way handshake)
- Documented how to recognise suspicious traffic (SYN floods/port scans, DNS tunnelling, cleartext credentials, ARP spoofing, beaconing)
- Reflected on what a larger network needs beyond this: VLAN segmentation, IDS/IPS, SIEM logging, MFA, patch management

**Deliverable:** [`Task1_Network_Security_Report.pdf`](./Task1_Network_Security/Task1_Network_Security_Report.pdf) — full write-up with all 7 screenshots embedded.

**Reproduce it yourself:** see [`LAB_STEPS.md`](./Task1_Network_Security/LAB_STEPS.md).

---

## Task 2 — Web Application Security

**Goal:** Find and manually exploit common web vulnerabilities, then document the fix for each.

**Tools used:** Burp Suite Community Edition (already on Kali — no install needed) against **Altoro Mutual** (`demo.testfire.net`), IBM's public, intentionally-vulnerable demo bank — used in place of OWASP ZAP + WebGoat, which would have needed extra downloads and storage this setup didn't have.

**Findings:**

| Vulnerability | Where | How it was triggered |
|---|---|---|
| **SQL Injection** | Login form | Username `admin' --` bypassed the password check entirely and logged in as Admin |
| **Reflected XSS** | Search box | `<script>alert(1)</script>` executed directly in the browser |
| **CSRF** | Admin pages (add account / change password / add user) | Forms submit sensitive actions with only the session cookie — no anti-CSRF token anywhere in the form or the POST request |

**Mitigations documented for each:**
- SQLi → parameterised queries / prepared statements, least-privilege DB accounts
- XSS → context-aware output encoding, Content-Security-Policy, HttpOnly + Secure cookies
- CSRF → per-request anti-CSRF tokens, SameSite cookies, re-authentication on sensitive actions

**Deliverable:** [`Task2_WebApp_Security_Report.docx`](./Task2_WebApp_Security/Task2_WebApp_Security_Report.docx) — full write-up with all 7 screenshots embedded.

**Details & evidence index:** see [`Task2_WebApp_Security/README.md`](./Task2_WebApp_Security/README.md).

---

## Skills Demonstrated

`Network Security` · `Firewall Configuration` · `Wireshark / Traffic Analysis` · `Web Application Security` · `Burp Suite` · `SQL Injection` · `Cross-Site Scripting (XSS)` · `CSRF` · `Vulnerability Assessment` · `Linux (Kali)` · `Technical Documentation`

## Note on Tooling

Where the original task brief named a specific tool (OWASP ZAP, WebGoat) that wasn't available without extra installs on this setup, an equivalent live tool/target was used instead (Burp Suite + Altoro Mutual) — same vulnerability classes, same manual-exploitation methodology, documented in each task's own README.

## License / Ownership

All work in this repository was produced for and belongs to Redynox as part of the internship terms. Shared here publicly for portfolio purposes with Redynox's task format as context.
