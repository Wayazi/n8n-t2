# n8n with Ngrok Integration Example

## Docker Compose Configuration

```yaml
services:
  n8n:
    image: n8nio/n8n:latest
    restart: unless-stopped
    ports:
      - "${N8N_PORT}:5678"
    environment:
      - NGROK_AUTHTOKEN_FILE=/run/secrets/ngrok_authtoken
      - N8N_HOST=${N8N_HOST}
      - N8N_PORT=${N8N_PORT}
    secrets:
      - ngrok_authtoken
      - n8n_basic_auth_user
      - n8n_basic_auth_password

secrets:
  ngrok_authtoken:
    file: .secrets/ngrok_authtoken
  n8n_basic_auth_user:
    file: .secrets/n8n_basic_auth_user
  n8n_basic_auth_password:
    file: .secrets/n8n_basic_auth_password
```

## Ngrok Configuration (ngrok.yml)

```yaml
version: "2"
authtoken: your_authtoken_here  # Store actual token in .secrets/ngrok_authtoken
tunnels:
  n8n:
    addr: 5678
    proto: http
    schemes: ["https"]
    hostname: "your-custom-domain.ngrok-free.app"
```

## Security Best Practices
1. Store actual authtoken in `.secrets/ngrok_authtoken`
2. Set file permissions: `chmod 600 .secrets/* ngrok.yml`
3. Keep all sensitive files in `.gitignore`
4. Use HTTPS and Basic Auth for all external access