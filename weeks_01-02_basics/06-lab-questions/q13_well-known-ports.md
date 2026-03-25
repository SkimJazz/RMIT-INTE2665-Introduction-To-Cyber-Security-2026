# 13. Well-Known Network Ports

## Question:

Discuss some well-known ports used for providing network services (e.g., `ssh, ftp, mail, http, https, mysql`).
As an example, use below command to see, on **which port `mysql` should be running**.

```bash
cat /etc/services | grep mysql
```

## Bro! What's that mean?

Basically, discuss the following well-known ports for common services. And track down the port number
for MySQL using the command provided.

Discuss:

- What the service does
- Which port it typically uses
- Why that port/service matters from a security perspective

## Commands used:

```zsh
cat /etc/services | grep mysql
```

## Example Usage | Output:

What port is MySQL running on?

```zsh
┌──(kali㉿kali)-[~]
└─$ cat /etc/services | grep mysql

mysql           3306/tcp                        # MySQL Database Service
mysql-proxy     6446/tcp                        # MySQL Proxy
```

### Well-Known Ports Overview

#### 1️⃣ SSH — Port 22 (TCP)

```zsh
# Service: Secure Shell
# Purpose: Remote login and administration

ssh → 22/tcp
```

**Why it matters**

- Provides full remote access
- Common brute-force target
- Often the first service attackers probe

**Security considerations**

- Strong passwords or key-based auth
- Disable root login
- Sometimes moved to a non-default port

#### 2️⃣ FTP — Port 21 (TCP)

```zsh
# Service: File Transfer Protocol
# Purpose: File transfer (legacy)

ftp → 21/tcp
```

**Why it matters**

- Sends credentials in clear text
- Rarely used securely toda

**Security considerations**

- Should be avoided
- Replaced by SCP / SFTP
- Often blocked by default

#### 3️⃣ Mail Services (Multiple Ports)

Mail is split across functions, not one port.

```zsh
| Service | Port    | Purpose         |
| ------- | ------- | --------------- |
| SMTP    | 25/tcp  | Sending mail    |
| POP3    | 110/tcp | Retrieving mail |
| IMAP    | 143/tcp | Retrieving mail |
```

**Why it matters**

- Frequent phishing vector
- Often exposed externally
- Sensitive user data

#### 4️⃣ HTTP — Port 80 (TCP)

```zsh
# Service: Web traffic (unencrypted)

http → 80/tcp
```

**Why it matters**

- Common web service port
- Traffic readable in plaintext

**Security considerations**

- Should redirect to HTTPS
- Vulnerable to sniffing and MITM

#### 5️⃣ HTTPS — Port 443 (TCP)

```zsh
# Service: Secure web traffic

https → 443/tcp
```

**Why it matters**

- Encrypts data in transit
- Most modern web apps use this

**Security considerations**

- Certificates must be valid
- Misconfiguration still leads to attacks

#### 6️⃣ MySQL — Port 3306 (TCP)

```zsh
# Service: Database server

mysql → 3306/tcp
```

**Why it matters**

- Holds sensitive data
- Often mistakenly exposed

**Security considerations**

- Should not be internet-facing
- Restricted to localhost or internal network
- Strong authentication required

## Key Points:

- Knowing well-known ports helps identify services running on a system.
- Attackers often scan for these ports to find vulnerabilities.
- Properly securing services on these ports is crucial to protect against unauthorized access and data breaches.
- Understanding port usage aids in network monitoring and incident response.
- Helps in configuring firewalls and access controls effectively.
- Awareness of these ports is essential for both offensive and defensive cybersecurity strategies.
- Many security tools and scanners rely on knowledge of well-known ports to assess system security.
- Misconfigured services on these ports can lead to significant security risks.

## Why this matters in Security:

**Ports = doors**

**Services = what’s behind the door**

Security is about:

- Which doors are open
- What’s behind them
- Who is allowed to knock

You’re learning how to label the doors before you start locking them.

## Discussion:

_Well-known ports are standardised port numbers assigned to common network services. For example, SSH uses port 22 for secure remote access, HTTP and HTTPS use ports 80 and 443 for web services, and MySQL uses port 3306 for database access. Understanding these ports is important for identifying running services, assessing attack surfaces, and applying appropriate security controls._
