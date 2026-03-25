# 1. Create a New User Account

Create a new user named `gemma` with a home directory and Bash shell:

```bash
sudo useradd -m gemma -s /bin/bash
```

Set a password for the user:

```bash
sudo passwd gemmi
```
 

### 1️⃣ User accounts are security boundaries

Linux (and Kali) is a multi-user operating system where each user has:

- Their own UID
- Their own home directory
- Their own permissions
- Their own authentication credentials

Creating a new user tests that you understand:

“Security is enforced by separation, not convenience.”


### 2️⃣ Root vs normal users (privilege separation)

In Kali:

- root = full control
- kali = normal user (with sudo rights)
- gemma = another normal user

By creating gemma, you demonstrate:

- You know not all users are equal
- You know how admins provision access

This is a core real-world sysadmin skill.

3️⃣ Authentication ≠ identity

The lab intentionally splits the task into two commands:

```zsh
sudo useradd -m gemma -s /bin/bash
sudo passwd gemma
```

Why? Because:

- useradd → creates identity
- passwd → creates authentication

These are separate layers.

In security terms:

- Identity = who you are
- Authentication = how you prove it

That separation matters a lot later (AD, IAM, PAM, Zero Trust).

You are demonstrating:

- Password hashing
- Secure credential storage
- Account authentication control


**Discussion**

_Creating a new user account demonstrates how Linux enforces separation between identities. Unlike changing the password of an existing user, creating a new user provisions a separate security context with its own permissions, home directory, and authentication credentials. This reflects real-world system administration practices where individual users are assigned least-privilege access rather than sharing accounts._