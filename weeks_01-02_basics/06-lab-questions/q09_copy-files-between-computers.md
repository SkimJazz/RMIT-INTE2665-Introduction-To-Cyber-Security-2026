# 9. Copy Files Between Computers (SCP)

## 1. Question

"Check how to copy files between two computers over the network. (Hint: `scp`)"

Below command will copy file.txt from your local computer (current folder) to another
computer on a specified IP address in `/remote/directory` folder using
remote_username

```bash
scp file.txt remote_username@10.10.0.2:/remote/directory
```

---

## 2. Bro! What’s that mean exactly?

The `scp` command is used to securely copy files between computers over a network using SSH for data
transfer and provides the same authentication and security as SSH.

The `command string` is saying, From the **current directory** on your local computer, take the file `file.txt` and
copy it to the remote computer at IP `10.10.0.2` in the `/home/remote_username/documents` directory.

Basically:

> **Learn how to securely send files between two machines using the command line, instead of unsafe methods like USB drives, shared folders, or plain copy-paste.**

More specifically:

- One computer has a file
- Another computer needs that file
- The transfer must be **secure**, **authenticated**, and **encrypted**

This is not just about copying files - it’s about **secure communication between systems**.

**Environments used for this question:**

- Control Host OS: Windows 11
- Guest OS: Kali Linux (VirtualBox VM)
- Netwoking: Bridged Adapter (In VirtualBox settings)
- Protocol: SSH (port 22)

---

## 3. Commands Used

**(In order of operation, end-to-end)**

### On Kali Linux

```bash
# Check SSH service status
sudo systemctl status ssh

# Start SSH service if inactive (if inactive, the terminal will show "inactive (dead)")
sudo systemctl start ssh

# Get Kali's IP address -> Remember to activate "Bridged Networking" in VM settings
ip a

# Bridge Network:
#   By default, VirtualBox uses NAT networking for VMs.
#   NAT blocks inbound connections from the host to the VM.
#   Switch to bridged networking so the host (Windows) can reach the VM (Kali) directly.
#   Look for `inet` under the bridged network interface (e.g., eth0, enp0s3)
#   Example: inet 192.168.1.100/24

# List files on Desktop to verify transfer
ls ~/Desktop
```

### On Windows PowerShell

```powershell
# Connect to Kali via SSH to verify access
ssh kali@<KALI_IP>

# Copy files between Windows and Kali
scp "C:\path\to\file.txt" kali@<KALI_IP>:/home/kali/Desktop/

# Copy files from Kali to Windows Desktop
scp kali@<KALI_IP>:/home/kali/Desktop/file.txt "$desktop\folder"

# Copy folders from Kali to Windows Desktop (recursive)
scp -r kali@<KALI_IP>:/home/kali/Desktop/folder "$desktop"
```

Optional but useful:

```powershell
# Get Windows Desktop path
$desktop = [Environment]::GetFolderPath('Desktop')

# Verify Desktop path exists -> Prints True if exists
Test-Path $desktop

# $desktop: may not work in newer PowerShell versions (7+); use full path instead
```

---

## 4. Example Usage | Output

### Example: Windows → Kali

```powershell
# File transfer from Windows desktop to Kali desktop
scp "C:\Users\My Computers Name\Desktop\fileTransfer.txt" kali@xxx.xxx.xx.x:/home/kali/Desktop/

# File transfer from within a dirctory(User defined) on Windows desktop to a directory(User defined) on Kali desktop
scp "C:\Users\My Computers Name\Desktop\transfer-windows\fileTransfer.txt" kali@xxx.xxx.xx.x:/home/kali/Desktop/transfer-kali/
```

> **REMEMBER!! Must use double quotes `""` around Windows paths with spaces.**
> E.g. There are spaces in `My Computers Name`. So the path must include quotes

**Result on Kali:**

```bash
ls ~/Desktop

# Output:
fileTransfer.txt
```

---

### Example: Kali → Windows

```powershell
# File transfer from Kali desktop to Windows desktop
scp kali@xxx.xxx.xx.x:/home/kali/Desktop/fileTransfer.txt "$desktop\transfer-windows"

# Or, using full file path instead of `$desktop` variable:
# File transfer from within a directory on Kali desktop to a directory on Windows desktop
scp kali@xxx.xxx.xx.x:/home/kali/Desktop/transfer-kali/fileTransfer.txt "C:\Users\My Computers Name\Desktop\transfer-windows"

# There are a few things to note here:
# 1. The destination path on Windows(PowerShell) ends with the folder name 'transfer-windows'and no backslash.
#    This means the file will be copied INTO that folder, keeping its original name.
#    Adding a backslash(\) at the end will make PowerShell throw-up (think it's a folder).
# 2. If you wanted to rename the file during transfer, you could specify a new filename at the destination:
# Example:

# Renaming file during transfer from Kali(desktop) to Windows(desktop):
scp kali@xxx.xxx.xx.x:/home/kali/Desktop/fileTransfer.txt "C:\Users\My Computers Name\Desktop\fileTransfer-NewName.txt"
```

**Result on Windows:**

```
Desktop/
└── transfer-windows/
    └── fileTransfer.txt
```

---

### Example: Folder transfer (recursive)

```powershell
# Folder transfer from Kali desktop to Windows desktop:

# This command copies the entire 'transfer-kali' folder from Kali Desktop to Windows Desktop
scp -r kali@xxx.xxx.xx.x:/home/kali/Desktop/transfer-kali "$desktop"
```

---

## 5. Gotchas | Common Mistakes

> The OG question involves networking, operating systems, and command-line tooling. As a result, several non-obvious issues may occur when using `scp` for the first time.

### ❗ SSH connection timeout (`port 22: Connection timed out`)

**Cause:**
Kali Linux VM was using **NAT networking**, which blocks inbound SSH connections.

**Fix:**
Configure the VirtualBox network adapter to **Bridged Adapter** so the host can initiate connections to the VM.

---

### ❗ Running `scp` from the wrong terminal

**Cause:**
Attempting to run `scp` from the Kali terminal while referencing **Windows paths** (e.g. `C:\Users\...`).

**Fix:**

- Use **Windows PowerShell** when copying files to/from Windows
- Use **Linux paths** only when running commands inside Kali

---

### ❗ File not found on Windows

**Cause:**

- Missing file extension (`.txt`, `.pdf`, etc.)
- Windows Explorer hides extensions by default
- Desktop path redirected by OneDrive

**Fix:**
Verify the exact filename using:

```powershell
dir
```

and confirm the real Desktop path.

---

### ❗ PowerShell stuck at `dquote>`

**Cause:**
An opening double-quote (`"`) was entered without a matching closing quote.

**Fix:**
Press `Ctrl + C` and re-enter the command carefully.

---

### ❗ Extra quote appearing in error output (`Desktop""`)

**Cause:**
A **trailing backslash inside a quoted Windows path**, for example:

```powershell
"C:\Users\...\Desktop\folder\"
```

**Fix:**
Remove the trailing backslash when using quotes:

```powershell
"C:\Users\...\Desktop\folder"
```

---

### ❗ File appears renamed after transfer

**Cause:**
The destination path explicitly included a filename.

**Clarification:**
Renaming is **optional**, not required.
If the destination is a directory, the original filename is preserved automatically.

---

### ❗ Folder transfer fails

**Cause:**
`scp` copies **files only** by default.

**Fix:**
Use the recursive flag when copying directories:

```powershell
scp -r source destination
```

---

### ❗ Kali ↔ WSL Ubuntu connection issues

**Cause:**
VirtualBox (Bridged) and WSL2 (NAT) use different networking models.

**Resolution:**
Use **Windows as the intermediary host** rather than connecting Kali directly to WSL.

---

### ❗ Concern about exposing the Kali IP address

**Clarification:**
Private IP addresses (e.g. `192.168.x.x`) are **not internet-routable** and do not expose the system externally.

---

## 6. Why `scp` matters in Security

- Encrypts file transfers in transit
- Prevents credential and data sniffing
- Commonly used for:
  - Secure key exchange
  - Incident response evidence transfer
  - Administrative access to servers

Secure file transfer is **foundational** in cyber security.

Real-world examples:

- Sending encryption **public keys**
- Receiving **encrypted evidence**
- Moving files during **incident response**
- Administering **remote servers**

`scp` provides:

- 🔐 Encryption (via SSH)
- 🔑 Authentication
- 📦 Integrity of data in transit

In **Assessment-1**, this exact skill is required when:

- Sending a public key to _Alice_
- Receiving an encrypted file back

---

## 7. Key Points

**On the first connection:**

- Your Kali machine has no record of Windows SSH identity
- SSH refuses to assume trust automatically

**SSH uses host keys to prevent:**

- Man-in-the-middle attacks
- Impersonation of remote systems

**What was demonstrated?**

- Encrypted file transfer
- Remote authentication
- Controlled access to another system

**Some high-value exam facts/tips:**

- `scp` = **secure copy**
- Uses **SSH** (port 22)
- Data is **encrypted in transit**
- Syntax:

  ```bash
  scp source destination
  ```

- Copying folders requires `-r`
- Filename is preserved when destination is a directory
- Renaming only happens if explicitly specified
- NAT networking blocks inbound SSH
- Bridged networking allows host ↔ VM communication

If you remember _only one thing_:

> **Destination path controls filename behaviour — not the source.**

---

## 8. Discussion

Question 9 looks simple on paper, but it quietly introduces several **core security concepts**:

- Trust boundaries between systems
- Secure channels vs convenience shortcuts
- Authentication before data exchange
- The difference between _working_ and _working securely_

The troubleshooting involved (network mode, SSH reachability, path handling) mirrors real-world operational security work. Understanding _why_ something fails — not just how to fix it — is what turns a basic Linux command into a security skill.

This question also acts as a **bridge** (no pun intended) between introductory labs and Assessment-1, where secure key exchange is mandatory.

---
