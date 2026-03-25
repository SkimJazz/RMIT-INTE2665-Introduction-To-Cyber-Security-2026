# 8. Copy and Move Files Locally

## Question:

"Check how to copy and move files from one folder to another folder. (Hint: `cp` and `mv`)"

## Bro! What's that mean?

Use the `cp` command to copy files and the `mv` command to move (or rename) files.

Basically this question is testing basic file operations and checks that you understand the difference between:

- Copying `cp` → duplicating data
- Moving `mv`→ relocating data

That distinction is critical in:

- Incident response
- Forensics
- System administration

## Commands used:

```zsh
cp
mv
```

## Example Usage | Output:

### Copy a file:

```zsh
cp source_file source_files_new_name
```

Example:

The following command makes a copy of the file `note-1.txt` and names the copy `backup_note-1.txt` and stores it in the same directory as the original file:

```zsh
cp note-1.txt backup_note-1.txt
```

Broken down in plain English:

Basically this is saying, In the **current directory**, take the file `note-1.txt` and make a copy of it called `backup_note-1.txt`.

Components:

`cp`→ copy a file

`note-1.txt`→ source → “Take the file named note-1.txt”

`backup_note-1.txt`→ destination → “Create a new file named backup_note-1.txt as a copy of the source file”

### Move a file:

```zsh
mv source_file new_location/new_file_name
```

Example:

The following command moves the file `backup_note-1` from the directory `testFolder-1` to the directory `testFolder-2`:

```zsh
mv testFolder-1/backup_note-1 testFolder-2
```

Broken down in plain English:

Basically this is saying, In the `testFolder-1` directory, take the `backup_note-1` file and move(`mv`) it to the `testFolder-2` directory?

Components:

`mv`→ move (or rename) a file
`testFolder-1/backup_note-1`→ source → “Inside the testFolder-1 directory, take the file named backup_note-1”
`testFolder-2`→ destination → “Put it inside the testFolder-2 directory”

## Explanation:

## Why this matters in Security:

This knowledge feeds directly into:

- Log handling
- Malware sample isolation
- Backup procedures
- Secure file transfer (next question: scp)

## Summary | Key Points:

Key behavioural differences

| Command | Original File | New File | Risk   |
| ------- | ------------- | -------- | ------ |
| `cp`    | Remains       | Created  | Low    |
| `mv`    | Removed       | Created  | Higher |

This is why **forensics uses copy, not move**.

## Discussion:

_Files can be copied from one directory to another using the cp command, which creates a duplicate of the original file. Files can be moved or renamed using the mv command, which relocates the file and removes it from its original location. These commands are commonly used for file management and must respect file permissions._
