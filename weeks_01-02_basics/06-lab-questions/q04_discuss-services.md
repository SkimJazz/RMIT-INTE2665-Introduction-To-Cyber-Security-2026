# 4. Start and Stop Services (SSH, HTTP, MySQL)

Discuss how services such as SSH, HTTP, and MySQL are started and stopped.


_Services are managed independently. Services such as SSH, HTTP, and MySQL are managed by the system’s init system (systemd). They are started and stopped using service management commands such as `service` or `systemctl`. Each service runs independently as a background daemon and listens on its associated network port. Starting or stopping one service does not affect others. Managing services is important for system security because running services expose network ports and increase the system’s attack surface._

Start Apache (HTTP):

```bash
sudo service apache2 start
```

Stop Apache:

```bash
sudo service apache2 stop
```

**Key points to consider and understand:**

- Services run as background processes (daemons)
  - If a service is running → a port is open
  - Each service listens on its own network port
  - If a port is open → it can be attacked
- Starting/stopping one service does not affect others
- Services are attack surfaces
- Stopping a service = reducing attack surface

This becomes critical later with:

- Port scanning (nmap)
- Service enumeration
- Hardening exercises
- Incident response (“what was running?”)