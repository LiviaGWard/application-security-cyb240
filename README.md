# 🕵️ CYB-240: Application Security
**Southern New Hampshire University | Grade: A | Term: 2025 C-4 (Jun – Aug)**

> Hands-on application security course covering offensive and defensive techniques — real vulnerability scanning with OpenVAS, web server attacks, SQL injection, privilege escalation, command injection, WEP/WPA cracking, Metasploit/Armitage exploitation, and OWASP-based secure development recommendations. All labs performed in live virtual environments.

---

## 📋 Course Overview
This course took a penetration tester's perspective — learning how attacks work in order to defend against them. I performed real attacks in controlled lab environments using industry-standard tools (Kali Linux, Metasploit, OpenVAS, Armitage), then translated that knowledge into professional vulnerability reports and security recommendations grounded in OWASP standards and CVE data.

**Key tools:** OpenVAS, Metasploit, Armitage, Kali Linux, XAMPP, SQL injection techniques, Burp Suite concepts
**Key frameworks:** OWASP Top 10, OWASP Proactive Controls, CVE/CVSS scoring

---

## 📁 Repository Structure

```
application-security-cyb240/
│
├── projects/
│   ├── project-one-vulnerability-summary-report.md
│   ├── project-one-milestone-openvas-findings.md
│   ├── project-two-recommendations-report.md
│   └── project-two-stepping-stone-preliminary-report.md
│
├── labs/
│   ├── module-one-html-pentesting-perspective.md
│   ├── module-two-web-server-attack-wireless-cracking.md
│   ├── module-three-sql-injection.md
│   ├── module-four-privilege-escalation-html-injection.md
│   └── module-five-command-injection-metasploit.md
│
├── activities/
│   ├── module-one-basic-html.md
│   └── module-two-css-basics.md
│
└── README.md
```

---

## 📝 Projects

### 🔴 Project One — Vulnerability Summary Report (OpenVAS Scans)
Conducted vulnerability scans on three systems (Firewall, Ubuntu Server, Windows Server) using **OpenVAS** and produced a professional vulnerability summary report with CVE identification, real-world incident examples, and verified remediation evidence.

**Critical findings (CVSS 10.0):**
- **Firewall:** PHP `php_stream_scandir()` Buffer Overflow (CVE-2012-2688) — arbitrary code execution; TWiki XSS & Command Execution (CVE-2008-5304/5305)
- **Windows Server:** PHP Type Confusion DoS (CVE-2015-4601); Apache httpd Range Header DoS (CVSS 7.8)
- **Ubuntu Server:** OpenSSL End of Life — version 0.9.8l, no longer receiving security updates

**Remediation verified:** PHP upgraded to current version; OpenSSL updated to supported release.

---

### 🔴 Project Two — Recommendations Report (Secure Development)
Analyzed a financial services web application scenario and produced OWASP-grounded security recommendations for two critical vulnerabilities found in the development environment.

**Vulnerability 1: Broken Access Control**
- Risk: Client-side login scripting + Apache Tomcat internet exposure = bypassable authorization
- Recommendation: Server-side access control enforcement; "secure by default / default deny" design; role-based permissions validated on every request

**Vulnerability 2: Injection Attacks (SQL/XML)**
- Risk: PHP + PostgreSQL + weak XML metadata + unencrypted transactions = injection attack surface
- Recommendation: Complete mediation principle; prepared statements/ORM; whitelist input validation; TLS for all transactions

**Framework used:** OWASP Top 10 (2021), OWASP Proactive Controls

---

## 🗂️ Labs

### Module One — HTML from a Pentester's Perspective
Examined HTML source code from an attacker's viewpoint — identifying how exposed HTML structure, hidden fields, and form logic reveal application vulnerabilities before any exploit is attempted. Compared HTML vs. XHTML security implications.

**Key insight:** XHTML's stricter rules (mandatory DOCTYPE, lowercase tags, quoted attributes, proper nesting) produce more consistent, parseable code — reducing ambiguity that attackers can exploit in lenient HTML parsers.

---

### Module Two — Web Server Attack & Wireless Protocol Cracking
**Lab 1: Attacking Web Servers from the WAN**
- Performed a live web server attack, altering website content
- Covered attacker tracks by deleting lines in `access.log`

**Defensive analysis:**
- File integrity monitoring (FIM) detects unauthorized log modifications
- System-level audit logging tracks file access and changes
- Web Application Firewall (WAF) blocks common attack vectors before they reach the server
- IDS provides real-time alerts on suspicious network behavior

**Lab 2: Breaking WEP and WPA Encryption**
- Cracked WEP encryption using aircrack-ng methodology
- Cracked WPA using dictionary/brute-force attack
- Decrypted captured wireless traffic

**Key insight:** WEP is cryptographically broken and should never be used. WPA2/WPA3 with strong, unique passphrases is the minimum acceptable standard.

---

### Module Three — SQL Injection
**Lab 1: SQL Injection Analysis**
- Demonstrated classic SQLi password bypass using `' OR '1'='1`
- Analyzed how unescaped input allows attackers to manipulate SQL queries and bypass authentication

**How escaping mitigates SQLi:**
Input escaping treats special characters (like `'`) as literal values rather than executable SQL syntax. This means the injected payload is passed to the database as data — not as a command — preserving the intended query logic and blocking the bypass.

**Lab 2: SQL Injection — Data Theft & Backdoor Creation**
- Used SQL injection to steal data from a database
- Created a backdoor user account (Ward) via SQL injection
- Used Metasploit to exploit the compromised system

**Metasploit's defensive value:** Security analysts use Metasploit to simulate real-world attacks in controlled environments — testing defenses, identifying exploitable vulnerabilities, and understanding attacker methodology before real attackers do.

---

### Module Four — Privilege Escalation & HTML Injection
**Lab 1: Remote and Local Exploitation / Privilege Escalation**
- Performed privilege escalation from user-level to elevated/root access
- Demonstrated how low-privilege access can be leveraged for full system compromise

**Why privilege escalation matters:**
Privilege escalation allows attackers to execute critical commands, access sensitive data, install persistent backdoors, and compromise the entire system — starting from a foothold as low as a regular user account. Every unnecessary privilege granted to users or services expands this attack surface.

**Lab 2: HTML Injection (HTMLi) Vulnerability & Mitigation**
- Exploited an HTML injection vulnerability in a web application
- Implemented and verified a mitigation control

**Deprecated PHP risk:**
Web applications can mitigate deprecated PHP code by:
- Regularly updating PHP to the latest supported version
- Performing code audits to identify and replace deprecated functions
- Using automated static analysis tools to flag deprecated usage
- Monitoring PHP official deprecation notices and planning migrations proactively

---

### Module Five — Command Injection & Full Application Exploitation
**Lab 1: Command Injection**
- Injected OS commands through a vulnerable PHP web application
- Established a remote shell from the injected command
- Added custom HTML comment signature to modified code

**Interpreted vs. compiled language security risk:**
PHP (interpreted) executes code line-by-line at runtime — meaning:
- Source code is more easily exposed or readable
- Vulnerabilities can be discovered and exploited at runtime
- No compilation step means malicious input can be executed directly
- Generally slower than compiled languages with larger runtime attack surface

Compiled languages convert code to machine code at build time — making source harder to reverse and eliminating some runtime injection vectors.

**Lab 2: Exploiting a Vulnerable Web Application (XAMPP / Armitage)**
- Used **Armitage** (Metasploit GUI) to exploit a vulnerable XAMPP installation
- Achieved post-exploitation access and extracted credential files (Ward)

**XAMPP vulnerability:**
XAMPP's default configuration leaves administrative interfaces (phpMyAdmin, etc.) unsecured and accessible without authentication. This allows attackers to gain full database and server control without any credential exploitation — a critical misconfiguration that must be remediated before any production deployment.

---

## 💡 Key Concepts Mastered
- OpenVAS vulnerability scanning and CVE/CVSS interpretation
- SQL injection — bypass, data theft, backdoor creation, and mitigation (escaping, prepared statements)
- Command injection — exploitation and PHP security implications
- HTML injection and web application input validation
- Privilege escalation — techniques and defensive implications
- Web server attack methodology and log manipulation
- WEP/WPA wireless encryption cracking (aircrack-ng)
- Metasploit and Armitage — offensive tool use for defensive understanding
- OWASP Top 10 (2021) — Broken Access Control, Injection
- OWASP Proactive Controls — Secure by Default, Complete Mediation, Input Validation
- Web Application Firewall (WAF) deployment rationale
- File integrity monitoring for log protection
- Secure development lifecycle (SDLC) security integration

---

## 🛠️ Tools Used
- **OpenVAS** — vulnerability scanning
- **Kali Linux** — penetration testing platform
- **Metasploit / Armitage** — exploitation framework
- **aircrack-ng** — wireless encryption cracking
- **XAMPP** — vulnerable web application environment
- **PHP / HTML / CSS** — web application fundamentals
- **SQL** — injection analysis and mitigation

## 📚 References
- OWASP. (2021). OWASP Top Ten. https://owasp.org/www-project-top-ten/
- OWASP. (n.d.). OWASP Top Ten Proactive Controls. https://owasp.org/www-project-proactive-controls/
- CVE-2012-2688, CVE-2008-5304, CVE-2008-5305, CVE-2015-4601

## 📚 Course
- **CYB-240** — Application Security | Grade: A | SNHU 2025
