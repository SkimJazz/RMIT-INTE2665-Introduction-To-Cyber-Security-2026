# Week 3-4: Symmetric and Asymmetric Key Encryption using GPG

In this Lab, you are going to learn symmetric key encryption using an open-source tool called
`GnuPG`. The `GnuPG` (also known as `GNU Privacy Guard` or simply `GPG`) is GNU’s tool used to
encrypt data and create digital signatures that contribute to overall information security. It
is a complete and free implementation of the OpenPGP Internet standard that provides an advanced
key management solution. For more information, please visit: https://www.gnupg.org/

At the end of the Lab, we will learn the following:

- Setup the environment to use GPG.
- Sharing files between two users in Kali Linux.
- Symmetric Key Encryption & Decryption using GPG.

<br>

# Week 3 - Environment setup and Symmetric key encryption

## Task 1: Setup the environment to use GPG

> **Important instructions to work on GPG**.

Consider the below points when working with GPG.

> **All keys information must be saved in current user’s home folder, so never use sudo when using
> GPG commands**.

- When executing GPG commands, every user (Sender or Receiver) must login to Kali Linux outside
  (from host computer using ssh command) or should login from Switch User option from the UI.
- SSH client can be used to login to Kali Linux from host computer. SSH Client tool is by default
  installed on Windows and Mac.
- One of the requirements is that GPG agent must be initialized from the current user to use GPG
  commands. When a user login from outside (from host computer, using ssh command) or from switch
  user function from kali Linux UI, then GPG agent is automatically initialized. Otherwise, OS will
  show permission error.
- Secure Copy (scp) should be used to securely transfer files to the Kali Linux users.

### Task 1.1: SSH Services

The secure way to share files on Kali Linux is via scp (Secure Copy). Scp needs ssh service running
on the system. Run below commands as Kali User.

Enable ssh service as auto-start (when OS starts).

## Step 2: Check existing files in Alice's home directory

```bash
┌──(alice㉿kali)-[~]
└─$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  test.txt  test.txt.gpg  Videos
```

## Step 3: Remove existing test.txt file

```bash
┌──(alice㉿kali)-[~]
└─$ rm test.txt


gpg --no-symkey-cache --armor --output encrypt_sameFile.txt.gpg --symmetric --cipher-algo AES256 sameFile.txt
```

## Step 4: Check files again to confirm deletion

```bash
┌──(alice㉿kali)-[~]
└─$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  test.txt.gpg  Videos
```

## Step 5: Decrypt the received encrypted file (test.txt.gpg)

```bash
┌──(alice㉿kali)-[~]
└─$ gpg --no-symkey-cache -o decrypted_test.txt -d test.txt.gpg
gpg: AES256.CFB encrypted data
gpg: encrypted with 1 passphrase
```

## Step 6: View the contents of the decrypted file

```bash
┌──(alice㉿kali)-[~]
└─$ cat decrypted_test.txt
This is my first encryption
```

<br>

# Week 4 - Asymmetric / public key encryption

In this part of the Lab, you are going to learn asymmetric / public key encryption and decryption
using an open-source tool called GnuPG. We assume that you have already practised symmetric key
encryption using GPG in Week 4. Please refer to Week 4 lab if you have not practised that yet.
For more information on GPG, please visit: https://www.gnupg.org/

## Task 1: Asymmetric / Public Key Encryption using GPG

In this task, you will use two users of Kali Linux: kali (the default user) and alice (that you
have already created in previous labs). If you have not created any user in your Kali Linux yet,
refer to previous weeks’ labs.

We will consider the following scenario:

- There are two users in your Kali Linux: **kali** and **alice**.
- The user **kali** is the **sender** and **alice** is the **recipient**.
- The user **kali** has a file “test.txt” that contains a secret message “Top Secret”.
- The user **kali** encrypts the file “test.txt” using **alice**’s RSA public-key using GPG.
- The encrypted file is then sent to the user **alice**.
- The user **alice** decrypts the encrypted file using **alice**’s RSA private key.

### Task 1.1: Create text file

Login as a `Kali` user and create a file “`test.txt`” in the Desktop directory and put the text
**“Top Secret”** in the file.

```bash
┌──(kali㉿kali)-[~]
└─$ echo "Top Secret" > test.txt
```

Check if the file has been created successfully.

```bash
┌──(kali㉿kali)-[~]
└─$ ls test.txt
test.txt
```

### Task 1.2: Generate RSA key-pair in GPG for the recipient Alice

As discussed in the lecture, public-key encryption algorithm requires two keys: **public**
and **private** keys.

Login as the user **alice** (using `ssh` command from host computer, see previous lab for details).

#### Login as Alice form Host computer using SSH

```powershell
# kali's => alice's SSH connection from Windows -> IP masked for security
PowerShell 7.5.4
PS C:\Users\My Computer> ssh alice@xxx.xxx.xx.x
alice@xxx.xxx.xx.x's password: ********
Linux kali 6.16.8+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 6.16.8-1kali1 (2025-09-24) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Tue Jan 27 23:55:32 2026 from xxx.xxx.xx.x
```

#### Use GPG to generate RSA key-pair for Alice

Using `gpg --full-generate-key` command (Remember! We are using PowerShell on host computer to login as
alice on Kali Linux VM), generate an RSA key-pair for the user **alice** with the following parameters:

- Key type: RSA and RSA
- Key size: 1024 bits
- Key validity: Never expires

```bash
# Start the generation of the RSA key-pair
┌──(alice㉿kali)-[~]
└─$ gpg --full-generate-key

# Output:
gpg (GnuPG) 2.4.8; Copyright (C) 2025 g10 Code GmbH
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

# RSA and RSA (1) key type selection in this case is used for both signing and encryption.
Please select what kind of key you want:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (sign only)
  (14) Existing key from card

# Selecting option 1 for RSA and RSA
Your selection? 1

# Enter in the size of 1024 bits for RSA key
RSA keys may be between 1024 and 4096 bits long.
What keysize do you want? (3072) 1024
Requested keysize is 1024 bits

# Selecting 0 for key validity means the key does not expire.
Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days      # Expiration times: days, weeks, months, years
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all

# Yep! I'm sure about that => y
Is this correct? (y/N) y

# Input user ID information for the key.
GnuPG needs to construct a user ID to identify your key.

Real name: Alice
Email address: alice@email.com
Comment: This is a RSA key of Alice
You selected this USER-ID:
    "Alice (This is a RSA key of Alice) <alice@email.com>"

Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O

# ----------- Terminal Prompts Below This Line --------------------- #
# PASSPHRASE popup prompt:
# Terminal will ask you to enter a passphrase to protect the private key.
# You will need to enter this passphrase whenever you use the private key.
# ------------------------------------------------------------------ #

# Entropy generation message during key creation.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
We need to generate a lot of random bytes. It is a good idea to perform
some other action (type on the keyboard, move the mouse, utilize the
disks) during the prime generation; this gives the random number
generator a better chance to gain enough entropy.
gpg: /home/alice/.gnupg/trustdb.gpg: trustdb created
gpg: directory '/home/alice/.gnupg/openpgp-revocs.d' created
gpg: revocation certificate stored as '/home/alice/.gnupg/openpgp-revocs.d/D1DB1DBA0F79C87EBBD8D1DE9E1BA9DAF28ABA32.rev'
public and secret key created and signed.

# GPG displays the key fingerprint after creation.
pub   rsa1024 2026-01-28 [SC]
      D1DB1DBA0F79C87EBBD8D1DE9E1BA9DAF28ABA32
uid                      Alice (This is a RSA key of Alice) <alice@email.com>
sub   rsa1024 2026-01-28 [E]
```

#### Verify the created key-pair

The keys are generated in a hidden directory `.gnupg`, which is in **alice’s home directory**.
You can view it by navigating to the user root’s home directory by typing below command.

```bash
# In the home(~) directory, check if the .gnupg directory is created
┌──(alice㉿kali)-[~]
└─$ ls -a
.                   .face          .vboxclient-clipboard-tty8-control.pid
..                  .face.icon     .vboxclient-clipboard-tty8-service.pid
.bash_history       .gnupg         .vboxclient-draganddrop-tty8-control.pid
.bash_logout        .ICEauthority  .vboxclient-hostversion-tty8-control.pid
.bashrc             .java          .vboxclient-seamless-tty8-control.pid
.bashrc.original    .local         .vboxclient-vmsvga-session-tty8-control.pid
.cache              Music          Videos
.config             Pictures       .Xauthority
decrypted_test.txt  .profile       .xsession-errors
Desktop             Public         .zprofile
.dmrc               .ssh           .zshrc
Documents           Templates
Downloads           test.txt.gpg
```

### Task 1.3: Making RSA Public key of Alice available to other users

To communicate with others, public key of **alice** should be exported. Use the following command
to export the public key in text format (the default is binary format):

So,basically you are exporting the public key of Alice to a file named `alice_public.txt` in ASCII
armored format.

```bash
# Export the public key in ASCII armored format to a file named alice_public.txt
┌──(alice㉿kali)-[~]
└─$ gpg --export --armor alice@email.com > alice_public.txt
```

**A few things are happing here:**

`--export`: This option tells GPG that you want to export a key (Public key).

- You specify which key to export by providing the associated email address.
- By default, this will export the public key in binary unless additional options are provided.

`-a or (--armor)`: This option tells GPG to create ASCII-armored output instead of binary output.

- ASCII armor is a text-based encoding that allows the public key to be easily shared via email
  or text files.

`alice@email.com`: This specifies the user ID of the key to be exported.

- GPG uses email addresses or other identifiers to locate the key within the keyring.

`> alice_public.txt`: This is the name of the file where the exported public key will be saved.

- The `>` alice_public.txt part of the command ensures that the output is written to this file.

#### Send the exported public key to the original account (kali) using SCP

```bash
# Send the exported public key file to the original account (kali) using SCP.
┌──(alice㉿kali)-[~]
└─$ scp alice_public.txt kali@localhost:
kali@localhost's password: ********
alice_public.txt                                        100% 1071   478.5KB/s   00:00
```

## Task 1.4: Importing RSA Public key of **alice** by the user **kali**

What this saying is:

First Login as User kali from your host computer using `ssh` command.

> I've been using kali on VirtualBox as the kali user and PowerShell on the host computer for user alice.

So, We are assuming that you have shared the public key file to the user kali and the file is
currently in the home directory (`/home/kali or ~`). Now, use the following command to import the
public key file into the user kali’s key-ring:

#### Import the public key file from alice into kali's key ring

```bash
┌──(kali㉿kali)-[~]
└─$ gpg --import alice_public.txt

# Output:
gpg: /home/kali/.gnupg/trustdb.gpg: trustdb created
gpg: key 9E1BA9DAF28ABA32: public key "Alice (This is a RSA key of Alice) <alice@email.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

#### check if the public key is in user kali's key ring

```bash
┌──(kali㉿kali)-[~]
└─$ gpg --list-keys

# Output:
/home/kali/.gnupg/pubring.kbx
-----------------------------
pub   rsa1024 2026-01-28 [SC]
      D1DB1DBA0F79C87EBBD8D1DE9E1BA9DAF28ABA32
uid           [ unknown] Alice (This is a RSA key of Alice) <alice@email.com>
sub   rsa1024 2026-01-28 [E]
```

**Alice's public key is now successfully imported into kali's key ring.**

### Task 1.5: File encryption by the user ‘kali’

Now, the user **kali** will encrypt the file ‘**test.txt**’ using alice’s public key (accessed using
Alice’s key-id: alice@email.com) and generate an encrypted file with a name ‘**encrypted_test.txt**’.
The command is as below:

`gpg --encrypt --armor --output encrypted_test.gpg --recipient alice@email.com test.txt`

```bash
┌──(kali㉿kali)-[~]
└─$ gpg --encrypt --armor --output encrypted_test.gpg --recipient alice@email.com test.txt

# Output:
gpg: 1784EBFEE07FE41E: There is no assurance this key belongs to the named user

sub  rsa1024/1784EBFEE07FE41E 2026-01-28 Alice (This is a RSA key of Alice) <alice@email.com>
 Primary key fingerprint: D1DB 1DBA 0F79 C87E BBD8  D1DE 9E1B A9DA F28A BA32
      Subkey fingerprint: 8817 8C47 E612 C8C5 807B  437D 1784 EBFE E07F E41E

It is NOT certain that the key belongs to the person named
in the user ID.  If you *really* know what you are doing,
you may answer the next question with yes.

# Chosing to use the key anyway => y
Use this key anyway? (y/N) y

# After chosing (y), the encryption process completes without further output.
# But the encrypted file should show up in kali's home directory.
```

**There are a few things happening here:**

- `--encrypt`: This option tells **gpg** to encrypt the specified file.
- `-a (--armor)`: This option tells GPG to create ASCII-armored output, which means the encrypted output will be in a text format rather than binary. This can be useful for transferring encrypted files via text-based mediums such as email.
- `--output encrypted_test.gpg`: This specifies the name of the file where the encrypted output will be saved. In this case, the encrypted content will be written to encrypted_test.txt.
- `--recipient alice@email.com`: This option specifies the recipient of the encrypted file. GPG will look for the public key associated with alice@email.com in your keyring and use it to encrypt the file. Only the private key corresponding to this public key can decrypt the file.
- `test.txt`: This is the name of the file to be encrypted. GPG will read the contents of this file, encrypt it, and then write the encrypted data to the output file specified by the --output option.

#### Verify the encrypted file

```bash
┌──(kali㉿kali)-[~]
└─$ ls encrypted_test.gpg

# Output:
encrypted_test.gpg
```

#### View the contents of the encrypted file

```bash
┌──(kali㉿kali)-[~]
└─$ cat encrypted_test.gpg

# Output:
-----BEGIN PGP MESSAGE-----

hIwDF4Tr/uB/5B4BA/9SmOhgDvAJhUNyBZoqdgePgnXHJg+UgaQ9fxFslG6htpZy
q2abgWKYAYsLe5BToLGHaLvAV2BMmVItbaOutHBziEIWbCdKgU02H9hVn1uQcZxX
NPt5g+zEQlpYNI9uY66MtlEVdux1wp0obYiedsK49oXfuYqLMlzOMbrQJvmdNNJO
AUD2EUBMpWVL9XoJL2EGt7CWcbQF6YpiffkL8x9rC7iukHk26PYX1k9JVrZ8MKF6
ABVhWvNG+1nNJAlWYkIXOulPzwNX+5ND4LTyYX6u
=+vlK
-----END PGP MESSAGE-----
```

#### Send the encrypted file to Alice using SCP

Now, share / transfer the encrypted file **encrypted_test.gpg** to the user alice using scp.

```bash
┌──(kali㉿kali)-[~]
└─$ scp encrypted_test.gpg alice@localhost:

# Output:
alice@localhost's password: ********
encrypted_test.gpg                            100% 1.3KB   1.3MB/s   00:00
```

### Task-1.6: File Decryption by the user 'alice

Now login as user alice using ssh command from host computer or switch user from UI.

`ssh alice@x.x.x.x`
where `x.x.x.x` is the IP address of Kali Linux vm. Now, run the following command at the user alice’s side to decrypt the file ‘encrypted_test.txt’:

`gpg --output decrypted_test.txt --decrypt encrypted_test.gpg`

```bash
┌──(alice㉿kali)-[~]
└─$ gpg --output decrypted_test.txt --decrypt encrypted_test.gpg

# -------------------- Output Terminal Prompt  --------------------- #
# PASSPHRASE popup prompt:
# Terminal will ask you to enter the passphrase that you set while
# creating the RSA key-pair for Alice.
# You will need to enter this passphrase to decrypt the file.
# ------------------------------------------------------------------ #

# Output:
gpg: encrypted with rsa1024 key, ID 1784EBFEE07FE41E, created 2026-01-28
      "Alice (This is a RSA key of Alice) <alice@email.com>"

# Choose to overwrite existing file => y
File 'decrypted_test.txt' exists. Overwrite? (y/N) y
```

**There are a few things happening here:**

- `--output decrypted_test.txt`: This specifies the name of the file where the decrypted output will be saved. In this case, the decrypted content will be written to decrypted_test.txt.
- `--decrypt`: This option tells gpg to decrypt the specified file. GPG will use the appropriate private key from your keyring to decrypt the file.
- `encrypted_test.gpg`: This is the name of the file to be decrypted. GPG will read the contents of this encrypted file, decrypt it, and then write the decrypted data to the output file specified by the --output option.

#### Verify the decrypted file

```bash
┌──(alice㉿kali)-[~]
└─$ ls decrypted_test.txt

# Output:
decrypted_test.txt
```

#### View the contents of the decrypted file

```bash
┌──(alice㉿kali)-[~]
└─$ cat decrypted_test.txt

# Output:
Top Secret
```

## Task 2: Signing and verifying files using GPG

In this task we will sign and verify a file to ensure its authenticity and integrity. In this task
**"alice”** will sign a file and send the signed file to “kali” to verify it. Since kali has already
imported alice’s public key in his key-ring, he can verify the file signed from alice.

### Task 2.1: Signing the file by Alice

User alice will sign the decrypted file (from previous step).

`gpg --output decrypted_test.sig --sign decrypted_test.txt`

```bash
┌──(alice㉿kali)-[~]
└─$ gpg --output decrypted_test.sig --sign decrypted_test.txt
```

The output Will create a new file decrypted_test.sig in Alice's home directory. This new file
contains both the original content of decrypted_test.txt and the digital signature.

#### Verify the signed file was created

```bash
┌──(alice㉿kali)-[~]
└─$ ls decrypted_test.sig

# Output:
decrypted_test.sig
```

### Task 2.2: Transfer the Signed file to another user (kali)

So, user Alice will transfer the signed file to user kali using `scp` command.

`scp decrypted_test.sig kali@localhost:`

```bash
┌──(alice㉿kali)-[~]
└─$ scp decrypted_test.sig kali@localhost:

# Output:
kali@localhost's password: ********
decrypted_test.sig                                          100%  231   167.2KB/s   00:00
```

### Task 2.3: Verifying the signed file by user kali

User kali will verify the signed file (sent from alice).

`gpg --verify decrypted_test.sig`

```bash
┌──(kali㉿kali)-[~]
└─$ gpg --verify decrypted_test.sig

# Output:
gpg: Signature made Wed 28 Jan 2026 09:40:07 PM EST
gpg:                using RSA key D1DB1DBA0F79C87EBBD8D1DE9E1BA9DAF28ABA32
gpg: Good signature from "Alice (This is a RSA key of Alice) <alice@email.com>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: D1DB 1DBA 0F79 C87E BBD8  D1DE 9E1B A9DA F28A BA32
```

✅ "**`Good signature`**" means that the file has not been altered since it was signed by Alice, and
it confirms that the file was indeed signed by Alice, as her public key was used to verify the
signature.

So, in this lab you have successfully completed the following tasks:

- Setup the environment to use GPG.
- Sharing files between two users in Kali Linux.
- Symmetric Key Encryption & Decryption using GPG.
- Asymmetric / Public Key Encryption & Decryption using GPG.
- Signing and verifying files using GPG.
