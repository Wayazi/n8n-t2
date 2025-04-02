# n8n Security Best Practices

## Core Security Measures

1. **Secret Management**:
   - All sensitive credentials stored in `.secrets/` directory
   - Files automatically excluded from git via `.gitignore`
   - Includes:
     - ngrok_authtoken
     - n8n basic auth credentials
     - API keys

2. **File Permissions**:
   ```bash
   chmod 600 .secrets/* ngrok.yml .env
   ```

3. **Docker Security**:
   - Uses Docker secrets for credential injection
   - Runs with minimal required privileges
   - Includes health checks and resource limits

## Ngrok Security

1. **Authentication**:
   - Always use ngrok authtokens
   - Store tokens securely (not in version control)
   - Rotate tokens periodically

2. **Tunnel Security**:
   - Enforce HTTPS only
   - Use custom domains when possible
   - Implement Basic Auth for web interfaces

3. **Monitoring**:
   - Review ngrok logs regularly
   - Monitor for unusual traffic patterns
   - Set up alerts for authentication failures

## Implementation Checklist

- [ ] All secrets stored in `.secrets/` directory
- [ ] Proper file permissions set (600)
- [ ] ngrok.yml configured with HTTPS
- [ ] Basic Auth enabled for n8n
- [ ] Regular secret rotation schedule