# 12. View Services and Port Numbers

## Question:

“Try to find all the services that your system may provide and their associated port number.”
(Hint: `/etc/services`)

## Bro! What's that mean?

The `/etc/services` file is a reference file. It maps human-friendly service names to port numbers and protocols. This file is used by various networking programs to determine which port number to use for a given service.

Basically, the `/etc/services` is a reference file that associates service names (like HTTP, FTP, SSH) with their corresponding port numbers (like 80, 21, 22) and protocols (TCP/UDP).

It answers:

**"If a service were running, which port would it normally use?”**

Think of it as:

- A dictionary
- Not a live status report

## Commands used:

> NOTE: This is a read-only file, so you won't be starting or stopping services here. Instead, you'll just be looking at the list of services and their associated port numbers.
> AND, the **output is massive**, so you might want to use `less` or `grep` to filter through it.

```bash
cat /etc/services
```

## Example Usage | Output:

### Step 1️⃣ View the services file:

```zsh
# View the contents of the services file
cat /etc/services   # add | less  # to paginate the output
```

Here is a output snippet of what you might see:

```zsh
tcpmux          1/tcp                           # TCP port service multiplexer
echo            7/tcp
echo            7/udp
discard         9/tcp           sink null
discard         9/udp           sink null
systat          11/tcp          users
daytime         13/tcp
daytime         13/udp
netstat         15/tcp
qotd            17/tcp          quote
chargen         19/tcp          ttytst source
chargen         19/udp          ttytst source
ftp-data        20/tcp
```

### Step 2️⃣ Find specific services (Let's get realistic)

Instead of **all services**, the reasonable interpretation is:

> **Identify common services and their port numbers.**

Question 13 wants you to track down these ports:

- https
- ftp
- ssh
- mail (smtp, imap, pop3)
- mysql

Each line in the `/etc/services` file follows this format:

```zsh
service_name   port_number/protocol   [# comment]

http            80/tcp          # World Wide Web HTTP
https           443/tcp         # HTTP over SSL
ftp             21/tcp          # File Transfer Protocol
ssh             22/tcp          # Secure Shell
mysql          3306/tcp         # MySQL Database
```

## Explanation:

The `/etc/services` file is a plain text file that lists network services, their associated port numbers, and the protocols they use (TCP or UDP). Each line in the file typically contains the service name, port number/protocol, and an optional comment.

## Key Points:

What `/etc/services` actually contains

- Well-known ports
- Registered ports
- Both TCP and UDP mappings
- Human-readable service names

It doesn't do these things:

- Start services
- Stop services
- Indicate whether a service is running

## Why this matters in Security:

Knowing which services are associated with which ports is crucial for system administrators and security professionals. It helps in:

- Configuring firewalls
- Monitoring network traffic
- Identifying potential vulnerabilities
- Troubleshooting network issues

Attackers and defenders both rely on `/etc/services` to:

- Interpret scan results
- Identify expected service behaviour
- Correlate ports to applications during incident response

Example:

- Port 22 open → likely SSH
- Port 3306 open → likely MySQL

Even if the service is not running, the mapping matters.

IMPORTANT: Just because a port is listed in `/etc/services` does not mean that the service is currently running on your system. It simply indicates which port would be used if that service were active.

>So, **`/etc/services` tells you what ports mean, not what ports are open**.

## Discussion:

_The `/etc/services` file lists well-known network services and their associated port numbers. It acts as a reference for port-to-service mappings and does not indicate whether a service is currently running. By examining this file, common services such as SSH, HTTP, HTTPS, and MySQL and their default ports can be identified._
