# Task 2 — Web Application Security (Redynox Internship)

## What this covers
Testing Altoro Mutual (http://demo.testfire.net), IBM's public intentionally-vulnerable
demo bank, using Burp Suite Community Edition on Kali Linux. No app install was needed —
the target is hosted, and Burp was already on the system.

## Files
- `Task2_WebApp_Security_Report.docx` — full report (objective, steps, findings, mitigations)
- `screenshots/` — evidence, in the order used in the report:
  1. `01_burp_sitemap.png` — Burp Site map after browsing the target
  2. `02_sqli_payload_login.png` — login form with payload `admin' --`
  3. `03_burp_http_history_login.png` — intercepted login POST request in Burp
  4. `04_sqli_login_success.png` — logged in as Admin with no valid password
  5. `05_xss_payload_search.png` — search box with `<script>alert(1)</script>`
  6. `06_xss_alert.png` — the resulting JS alert popup
  7. `07_csrf_no_token_forms.png` — admin forms with no anti-CSRF token field

## Findings summary
| Vulnerability | Where | Payload / method |
|---|---|---|
| SQL Injection | Login form | `admin' --` as username, bypasses password check |
| XSS (reflected) | Search box | `<script>alert(1)</script>` executes in-browser |
| CSRF | Account admin forms (add account / change password / add user) | No token in form or POST — forgeable |

## Why testphp.vulnweb.com isn't used
It timed out on port 80 from this network (confirmed with `curl -I`). Altoro Mutual was
used instead — same three vulnerability classes, reachable target.

## Mitigations (short version)
- SQLi → parameterised queries, least-privilege DB user
- XSS → context-aware output encoding, CSP, HttpOnly/Secure cookies
- CSRF → per-request anti-CSRF token, SameSite cookies, re-auth on sensitive actions
