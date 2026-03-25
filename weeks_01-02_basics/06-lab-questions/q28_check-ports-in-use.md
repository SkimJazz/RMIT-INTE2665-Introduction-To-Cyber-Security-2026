# 28. Check Open Ports and Services

```bash
netstat -tulpn | grep :22
lsof -i tcp:22
nmap localhost
```
