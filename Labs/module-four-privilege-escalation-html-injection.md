# Module Four Labs: Privilege Escalation & HTML Injection
**CYB-240 | Application Security**

## Lab 1: Remote & Local Exploitation — Privilege Escalation

**Objective:** Perform privilege escalation from standard user access to elevated/root-level control and analyze its security implications.

### Steps Performed
- Gained initial foothold on target system with low-privilege user access
- Identified privilege escalation vulnerability
- Escalated from user-level to elevated/administrative access
- Verified escalated privileges at the command line

### What Is Privilege Escalation?
Privilege escalation refers to exploiting a vulnerability to gain unauthorized access to higher levels of permissions or system control — beyond what was originally granted.

**Two types:**
| Type | Description |
|---|---|
| **Vertical** | Low-privilege user gains admin/root access (most common and dangerous) |
| **Horizontal** | User gains access to another user's resources at the same privilege level |

### Why Security Specialists Must Prioritize This

Privilege escalation transforms a limited breach into a catastrophic one:
- **Execute critical commands** — attackers with admin/root can do anything the OS allows
- **Access sensitive data** — all files, databases, and credentials become accessible
- **Install persistent backdoors** — root-level persistence survives reboots and even reimaging in some cases
- **Disable security controls** — antivirus, logging, and monitoring can be turned off
- **Lateral movement** — elevated credentials enable attacks on other networked systems

**Common escalation vectors:**
- Unpatched kernel vulnerabilities
- Misconfigured SUID/SGID binaries (Linux)
- Weak service account permissions
- Stored credentials in plaintext config files
- Writable PATH directories

**Defensive mitigations:**
- Apply OS and kernel patches promptly
- Audit SUID/SGID binaries regularly
- Run services with minimal required privileges (Least Privilege)
- Monitor for unexpected privilege changes (audit logs, SIEM alerts)
- Implement endpoint detection and response (EDR) to flag escalation attempts

---

## Lab 2: HTML Injection (HTMLi) — Vulnerability & Mitigation

**Objective:** Exploit an HTML injection vulnerability in a web application, then implement and verify a working mitigation control.

### The Attack
HTML injection occurs when user-supplied input is rendered as raw HTML in the browser. Unlike XSS (which injects scripts), HTMLi injects HTML markup — but can still be used to:
- Redirect users to phishing pages
- Alter the visual appearance of the page (deface content)
- Create fake login forms to steal credentials
- Display misleading information to users

### The Mitigation
Implemented output encoding/escaping to prevent injected HTML from being interpreted by the browser. After the control was applied, the injected payload was displayed as literal text rather than rendered markup.

**Verification:** Confirmed the control worked — the injection attempt displayed the raw HTML characters on screen instead of executing.

### Deprecated PHP — Security Risk

**Key question: How can web applications mitigate the risk of deprecated PHP code?**

Deprecated PHP functions are removed from the language because they are insecure, unreliable, or replaced by better alternatives. If still in use, they represent known attack vectors that may have no available patches.

**Mitigations:**
- Regularly update PHP to the latest supported version
- Perform code audits targeting deprecated function usage
- Use automated static analysis tools (e.g., PHPStan, PHP_CodeSniffer) to flag deprecated calls
- Monitor the [PHP official deprecation notices](https://www.php.net/manual/en/migration.php) and plan migrations before end-of-life dates
- Enable PHP deprecation warnings in development environments so issues surface before production deployment

## Skills Demonstrated
`Privilege Escalation` `Vertical Privilege Escalation` `Root Access` `Least Privilege` `Linux Security` `HTML Injection` `Output Encoding` `Input Validation` `PHP Security` `Deprecated Code Risk` `EDR` `Audit Logging`
