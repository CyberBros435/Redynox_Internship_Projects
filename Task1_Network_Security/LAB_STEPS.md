# Task 1 Lab (do these, then screenshot, then paste into the report)
1. Windows Security > Firewall & network protection: Domain/Private/Public all ON. Screenshot -> 01_firewall_profiles.png
2. wf.msc > Inbound Rules > New Rule > Port > TCP 8888 > Block. Screenshot -> 02_block_rule.png
   Test: on laptop run `python -m http.server 8888`; from phone browser open http://<laptop-ip>:8888 -> should fail. (ipconfig for IP)
3. Router admin (192.168.x.1): change admin password + Wi-Fi password, security = WPA2-AES or WPA3, WPS off, remote admin off. Screenshot (hide secrets) -> 03_router_security.png
4. Wireshark: pick active Wi-Fi interface > start. Browse a few sites, `nslookup example.com`, open http://neverssl.com
   Filters: dns | http | tls | arp | icmp -> screenshots 04_dns.png 05_http.png 06_tls.png
5. Self-scan (ONLY your own second device): `nmap -sS <your-phone-or-VM-ip>`; Wireshark filter: tcp.flags.syn==1 && tcp.flags.ack==0 -> 07_syn_burst.png
6. Paste each screenshot at its red [INSERT SCREENSHOT] line, delete the placeholder text, fill the "[Add any real problem...]" bullet with what actually happened.
