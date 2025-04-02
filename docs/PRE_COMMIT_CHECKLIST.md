# Pre-Commit Security Checklist

## Critical Items to Verify
1. [ ] ngrok.yml does NOT contain actual authtoken
   - Should use: `authtoken: ${NGROK_AUTHTOKEN}`
2. [ ] .secrets/ngrok_authtoken contains the actual token
3. [ ] .gitignore includes:
   - ngrok.yml
   - .env
   - .secrets/

## Verification Steps
1. Check ngrok.yml:
```bash
grep -q "authtoken: [A-Za-z0-9_]" ngrok.yml && echo "SECURITY ALERT: Remove actual token!"
```

2. View staged changes:
```bash
git diff --cached
```

3. Commit only safe files:
```bash
git add README.md docs/ docker-compose.yml
git commit -m "Update documentation and configuration"
```

## Emergency Fixes
If secrets were accidentally committed:
1. Rotate all exposed credentials immediately
2. Rewrite git history to remove secrets
3. Force push to remote (if already pushed)