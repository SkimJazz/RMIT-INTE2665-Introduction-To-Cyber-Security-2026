# 11. Use `dig` for DNS Information

## Question:

"Use dig command and see what information you can find using it use RMIT's domain as an example."

```bash
dig rmit.edu.au
```

---

## Bro! What's that mean?

The `dig` command is a network administration command-line tool for querying Domain Name System (DNS) servers. It is used to retrieve information about domain names, such as IP addresses, mail servers, and other DNS records.

`dig` = Domain Information Groper

It’s a DNS query tool that lets you:

- Ask DNS servers questions directly
- See exactly what records are returned
- Bypass browser / OS abstractions

In security terms, it’s used for:

- Reconnaissance
- DNS troubleshooting
- Verifying DNS integrity

## Commands used:

```zsh
dig rmit.edu.au

# Other useful variations for Querying specific DNS records:
dig +short rmit.edu.au  # Get just the IP address
dig rmit.edu.au A      # Query A records (IPv4 addresses)
dig rmit.edu.au AAAA   # Query AAAA records (IPv6 addresses)
dig rmit.edu.au MX     # Query Mail Exchange records
dig rmit.edu.au NS     # Query Name Server records
```

## Example Usage | Output:

### Step 1: Run the basic command (as per lab)

```zsh
dig rmit.edu.au
```

** Output:**

```zsh
; <<>> DiG 9.20.15-2-Debian <<>> rmit.edu.au
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;rmit.edu.au.                   IN      A

;; ANSWER SECTION:
rmit.edu.au.            300     IN      A       131.xxx.x.xxx

;; Query time: 63 msec
;; SERVER: xxx.xxx.xx.x#53(xxx.xxx.xx.x) (UDP)
;; WHEN: Thu Jan 22 22:36:27 EST 2026
;; MSG SIZE  rcvd: 56
```

### Step 2: Understand the important sections

**HEADER section:**

```zsh
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
```

> Key points:
>
> - status: NOERROR → DNS query succeeded
> - Shows this was a standard query

**QUESTION section:**

```zsh
;; QUESTION SECTION:
;rmit.edu.au.                   IN      A
```

> Key points:
>
> - You asked for the A record
> - An A record maps a domain → IPv4 address

**ANSWER section:**

```zsh
;; ANSWER SECTION:
rmit.edu.au.            300     IN      A       131.xxx.x.xxx
```

> Key points:
>
> - The IP address(es) for the domain
> - 300 = TTL (seconds DNS can cache this result)

**AUTHORITY section:**

```zsh
AUTHORITY: 0
```

> Key points:
>
> - Empty here, but would list authoritative name servers for the domain
>   This helps identify:
> - Who controls DNS for the domain
> - Potential attack surfaces

**ADDITIONAL section:**

```zsh
ADDITIONAL: 1
```

> Key points:
>
> - This one has 1 additional record
> - Often contains extra info like related IPs

## Explanation:

Using the `dig` command with the various options allows you to gather detailed DNS information about a domain. This is crucial for network troubleshooting, security assessments, and understanding the infrastructure behind a domain.

So, from `dig` output, you can indentify:

- The IP address associated with the domain
- The type of DNS records available (A, AAAA, MX, NS, etc.)
- The authoritative name servers for the domain
- The TTL values for caching DNS responses
- Whether the DNS query was successful or if there were errors

## Why this matters in Security:

DNS is:

- A frequent attack target
- Used in phishing
- Used in command-and-control
- Often trusted too much

**If DNS lies, everything above it lies too. You’re learning how to verify, not assume.**

## Summary | Key Ponits:

- `dig` is a powerful DNS query tool
- It provides detailed DNS information
- Useful for troubleshooting and security assessments
- Helps identify potential vulnerabilities in DNS configurations

## Discussion:

_The `dig` command was used to query DNS information for a domain. It returned details such as IP addresses, DNS record types, time-to-live values, and authoritative name servers. This information is useful for understanding how domain names are resolved and for troubleshooting DNS-related issues._
