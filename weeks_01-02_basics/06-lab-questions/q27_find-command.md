# 27. Find Files

Files modified in last 5 days:

```bash
find / -mtime -5 -print
```

Search inside text files:

```bash
find / -name "*.txt" | xargs grep "svn"
```
