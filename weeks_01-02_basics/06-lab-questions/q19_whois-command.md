# 19. Domain Investigation with `whois`

Explore domain ownership and IP information:

```bash
whois rmit.edu.au
```

(Alternative web lookup tools may also be used.)

Love the momentum — **Question 19** is classic _reconnaissance 101_ and very exam-friendly. I’ll follow your agreed format exactly and load **Section 7 (Key Points)** with high-value exam facts.

---

## 1. Question

**“Explore a sample domain (e.g., rmit.edu.au) with `whois` command.
i. Pick a domain and whois that domain
ii. Try to find the IP of that domain.”**

---

## 2. Bro! What’s that mean exactly?

Linux is asking:

> “Who owns this domain, where is it registered, and what public information can I learn about it?”

This question is about **domain registration data**, _not_ live network scanning.

You are learning how to:

- Identify **domain ownership**
- See **registration and expiry details**
- Find **associated name servers**
- Discover **IP information indirectly**

---

## 3. Commands Used

```bash
whois rmit.edu.au
dig rmit.edu.au
```

Optional (web-based, as hinted in the lab):

- [https://whois.domaintools.com/rmit.edu.au](https://whois.domaintools.com/rmit.edu.au)

---

## 4. Example Usage | Output

### i️. `whois` the domain

```bash
whois rmit.edu.au
```

```bash
┌──(kali㉿kali)-[~]
└─$ whois rmit.edu.au

# Output: Example has been trimmed
Domain Name: rmit.edu.au
Registry Domain ID: 5488ab80dfd9488c840846d4b1692744-AU
Registrar WHOIS Server: https://whois.auda.org.au
Registrar URL: https://www.domainname.edu.au
Last Modified: 2025-08-25T00:12:41Z
Registrar Name: Education Services Australia Limited
Registrar Abuse Contact Email: registrar@esa.edu.au
Registrar Abuse Contact Phone: +61.399109829
Reseller Name: 
Status: serverRenewProhibited https://identitydigital.au/whois-status-codes#serverRenewProhibited
Status Reason: Not Currently Eligible For Renewal
Registrant Contact ID: bf7e149398b74a788dda16829ece86d2-AU
Registrant Contact Name: Domain Admin
Tech Contact ID: c08b7a0ede534846b9f67e6a259e1b74-AU
Tech Contact Name: Domain Admin
Name Server: ns1-external.rmit.edu.au

# ...more output...
# This section has been trimmed for brevity, but
# Under Name Server, you would see additional DNS servers and IP info.
# This particular search showed multiple name servers and IPs related to RMIT.
```

What this tells you:

- Who owns the domain -> **RMIT University**
- Which registrar manages it -> **Education Services Australia Limited**
- When it was registered -> **Not Currently Eligible For Renewal**
- When it expires -> **Last Modified: 2025-08-25**
- Which DNS servers manage it -> **ns1-external.rmit.edu.au**
- And more...

---

### ii️. Find the IP address of the domain

Whois **does not always directly list IPs**.
To reliably find the IP, use `dig`:

```bash
dig rmit.edu.au +short
```

Example output:

```text
131.xxx.xxx.xxx
```

This is the **current IPv4 address** returned by DNS.

---

## 5. Gotchas / Common Mistakes

- ❌ **Expecting whois to always show IP addresses**
  - Whois is about **registration**, not DNS resolution

- ❌ **Confusing domain owner with hosting provider**
  - Ownership ≠ where servers physically live

- ❌ **Assuming whois data is always accurate**
  - Privacy services and proxies are common

- ❌ **Using whois as a live scanning tool**
  - It’s passive, not active

---

## 6. Why whois` Matters in Security

`whois` is commonly used in:

- Reconnaissance
- Threat intelligence
- Incident response
- Phishing investigations

Security teams use whois to:

- Identify domain legitimacy
- Investigate suspicious domains
- Track domain age (new domains = higher risk)
- Correlate infrastructure ownership

Attackers also use whois — defenders need to understand it too.

---

## 7. Key Points

- `whois` retrieves **domain registration information**
- Shows **registrant, registrar, and expiry dates**
- Whois is **passive reconnaissance**
- Does **not** scan or contact the target system
- IP addresses are often found via **DNS (`dig`)**, not whois
- New or recently registered domains are **higher risk**
- Whois data may be **masked or anonymised**
- Common first step in **domain investigations**

**high-value exam facts/tips:**

- `whois` is about **ownership and registration**, not live scanning
- Use `dig` to find the **current IP address** of a domain
- Look for fields like **Registrant Contact** and **Registrar Name**
- Remember: **Not all whois data is public or accurate**

If a question mentions _“domain ownership”_ or _“registration details”_ → the answer is **`whois`**

---

## 8. Discussion

This question introduces a critical cyber-security mindset shift:

> Before attacking or defending a system, understand **who owns it and why it exists**.

`whois` doesn’t tell you _how_ a system works — it tells you **who is behind it**.
Combined with `dig`, it forms the foundation of **external reconnaissance**.

This is the same workflow used in:

- Phishing analysis
- Malware infrastructure tracking
- Threat actor attribution (at a basic level)
