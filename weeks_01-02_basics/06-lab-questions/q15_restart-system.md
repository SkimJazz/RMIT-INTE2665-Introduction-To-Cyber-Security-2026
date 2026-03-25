# 15. Reboot the System

## Question:

"Check how to restart the system with reboot command. Below command
will restart the system. `sudo reboot`".

System can also be rebooted from GUI from right click on Logged in User and clicking Shutdown option.

## Bro! What's that mean?

This is less about the command itself and more about:
- System control
- Administrative privilege
- Safe system lifecycle management

In short: who is allowed to restart a system, and how.

When you run the `sudo reboot` command, it performs the following actions:

- Terminates all running processes
- Unmounts file systems
- Shuts down the system
- Restarts the system, leading to a fresh boot-up sequence
  

## Commands used:

```bash
sudo reboot
```

## Example Usage | Output:

**What happens:**
- The system immediately begins a graceful shutdown
- Running services are stopped
- Filesystems are synced
- The system restarts

**This requires sudo because:**
- Restarting affects all users
- It is a privileged administrative action

## Key Points:

- Using `sudo` is important because rebooting the system requires administrative privileges.
- The `reboot` command is a controlled way to restart the system safely.
- Restarting the system is a common administrative task for applying updates or recovering from issues.

## Why this matters in Security:

Restarting a system is commonly used to:
- Apply updates
- Clear unstable states
- Recover from misconfiguration
- Complete kernel or service changes

From a security perspective:
- Unauthorized reboots = denial of service
- Therefore restricted to privileged users

## Discussion:

_The system can be restarted using the `sudo reboot` command, which performs a controlled shutdown and restart of the operating system. This command requires administrative privileges because it affects all users and running services. The system can also be restarted through the graphical user interface (GUI)._
