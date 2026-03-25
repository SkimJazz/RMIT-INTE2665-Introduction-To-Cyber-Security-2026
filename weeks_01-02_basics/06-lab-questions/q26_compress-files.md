## 26. Compress a Folder into Multiple Files

```bash
tar cz attachments/ | split -b 1m -a 2 -d - attachments.tgz_
```
