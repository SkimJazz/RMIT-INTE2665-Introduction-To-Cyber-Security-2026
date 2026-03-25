# 14. Lock and Unlock User Accounts

## Question:

Discuss how to lock or unlock a user to login the system.

Lock Tom out of the system:

```bash
sudo passwd -l tom
```

Let Tom back into the system (Unlock Tom):

```bash
sudo passwd -u tom
```

## Bro! What's that mean?

Basically, this is question is about account access control, not passwords themselves.

Specifically:

- How Linux prevents a user from logging in by locking their account
- How that restriction can be reversed to allow login again
- Why this is useful in security and administration

## Commands used:

```bash
# Lock Tom:
sudo passwd -l tom

# Unlock Tom:
sudo passwd -u tom

# Check if Tom is locked out:
sudo passwd -S tom
```

## Example Usage | Output:

### Locking a user account

```bash
sudo passwd -l tom
```

**What this does (important)**

- Locks the account
- Prevents the user from authenticating
- Does not delete the account
- Does not remove files or the home directory

Under the hood:

- Linux modifies the password hash in /etc/shadow
- The hash is prefixed so authentication always fails

👉 The user still exists, but cannot log in.

### Unlocking a user account

```bash
sudo passwd -u tom
```

**What this does**

- Removes the lock
- Restores the original password hash
- Allows the user to log in again (using the same password)

### Checking account status

```bash
sudo passwd -S tom

# Example output:
tom L 08/15/2023 0 99999 7 -1   # L = Locked
tom P 08/15/2023 0 99999 7 -1   # P = Password set (unlocked)
```

## Key Points:

| Action               | Account Exists | Can Login | Files Preserved  |
| -------------------- | -------------- | --------- | ---------------- |
| Lock (`passwd -l`)   | ✅ Yes         | ❌ No     | ✅ Yes           |
| Unlock (`passwd -u`) | ✅ Yes         | ✅ Yes    | ✅ Yes           |
| Delete (`userdel`)   | ❌ No          | ❌ No     | ❌ Often removed |

- Locking is reversible.
- Deletion is destructive.

**Locking users is about:**

- Access control
- Containment
- Least disruption

It’s safer than deletion and faster than password resets in many scenarios.

## Why this matters in Security:

Account locking is commonly used when:

- An employee leaves temporarily
- Suspicious activity is detected
- An account is under investigation
- Maintenance is being performed

It is a non-destructive containment control.

In incident response, locking accounts is often one of the first actions taken.

## Discussion:

_User accounts in Linux can be locked and unlocked using the passwd command. The passwd -l option locks a user account by disabling password authentication, preventing the user from logging in. The account and its files remain intact. The account can later be re-enabled using passwd -u. This approach is commonly used for temporarily disabling access without deleting the user account._
