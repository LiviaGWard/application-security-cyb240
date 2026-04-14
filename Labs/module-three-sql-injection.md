# Module Three Labs: SQL Injection
**CYB-240 | Application Security**

## Lab 1: SQL Injection — Analysis & Mitigation

**Objective:** Demonstrate SQL injection attack, then understand how input escaping mitigates it.

### The Attack: SQLi Password Bypass
Classic SQL injection using: `' OR '1'='1`

**How it works:**
A vulnerable login query looks like:
```sql
SELECT * FROM users WHERE username = '[input]' AND password = '[input]';
```

When an attacker inputs `' OR '1'='1` as the username:
```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '';
```

Since `'1'='1'` is always true, the entire WHERE clause evaluates to true — the query returns all users and grants access without valid credentials.

### The Defense: Input Escaping
**How escaping works:**
Input escaping treats special characters — like the single quote (`'`) — as literal data values rather than executable SQL syntax. The injected `'` is escaped to `\'`, which the database reads as a literal apostrophe character, not a string delimiter.

```sql
-- With escaping applied, the query becomes:
SELECT * FROM users WHERE username = '\' OR \'1\'=\'1' AND password = '';
-- The database reads this as a literal string search — no injection occurs
```

**Why it's successful:**
Escaping re-establishes the boundary between **data** and **code**. The application can now distinguish between user-supplied data and SQL syntax, so the injected payload is treated as harmless text rather than a command.

**Better solution — Prepared Statements:**
```php
// Prepared statement — injection-proof regardless of input
$stmt = $pdo->prepare("SELECT * FROM users WHERE username = ? AND password = ?");
$stmt->execute([$username, $password]);
```
Prepared statements separate SQL structure from data at the protocol level — user input can never become part of the query logic.

---

## Lab 2: SQL Injection — Data Theft & Backdoor Creation

**Objective:** Use SQL injection to steal database contents and create a persistent backdoor account, then use Metasploit to exploit the compromised system.

### Steps Performed
- Exploited SQL injection vulnerability to query database contents
- Used injection to create a new backdoor database user: **Ward**
- Leveraged Metasploit to exploit the compromised system post-injection

### Metasploit for Defensive Security
**Key question: How can Metasploit be used by security analysts defensively?**

Metasploit is one of the most powerful offensive tools available — and security analysts use it to:
- **Simulate real-world attacks** in controlled environments to test defenses before real attackers do
- **Identify exploitable vulnerabilities** by running the same payloads attackers would use
- **Validate patch effectiveness** — confirming an exploit no longer works after remediation
- **Understand attacker methodology** — knowing how an attack unfolds helps analysts detect it in progress
- **Test incident response procedures** — blue teams practice detection and containment against simulated Metasploit attacks

> *"Know your enemy."* — The best defenders understand offense.

### Key Takeaways
- SQL injection can go far beyond authentication bypass — database takeover, data theft, backdoor creation, and system compromise are all possible from a single injection point
- Defense requires both input validation AND prepared statements — escaping alone is insufficient if other injection vectors exist
- Any user-supplied input that touches a database query must be treated as untrusted

## Skills Demonstrated
`SQL Injection` `SQLi Password Bypass` `Input Escaping` `Prepared Statements` `Parameterized Queries` `Database Security` `Metasploit` `Backdoor Detection` `Data Exfiltration` `Kali Linux`
