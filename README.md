# n8n Workflow Automation with Ngrok Integration

This project sets up n8n workflow automation with secure ngrok tunneling for external access.

## Features
- n8n workflow automation platform
- Ngrok HTTPS tunneling with custom domain
- Docker-based deployment
- Secure configuration using environment variables and secrets

## Prerequisites
- Docker and Docker Compose
- Ngrok account with authtoken
- Basic Auth credentials for n8n

## Setup

1. Clone this repository
2. Configure your environment:
   ```bash
   cp .env.example .env
   cp .secrets/example/* .secrets/
   ```
3. Edit configuration files:
   - `.env` - Set basic configuration
   - `.secrets/n8n_basic_auth_user` - Set n8n username
   - `.secrets/n8n_basic_auth_password` - Set n8n password
   - `.secrets/ngrok_authtoken` - Set your ngrok authtoken
   - `ngrok.yml` - Configure your ngrok tunnel

4. Set file permissions:
   ```bash
   chmod 600 .env .secrets/* ngrok.yml
   ```

5. Start the services:
   ```bash
   docker compose up -d
   ```

## Security Considerations
- All sensitive files are excluded from git via `.gitignore`
- Secrets are stored in `.secrets/` directory with restricted permissions
- Ngrok provides HTTPS encryption for external access
- Basic authentication protects n8n web interface

## Usage
- Access n8n at: `https://[your-ngrok-domain].ngrok-free.app`
- Ngrok dashboard: https://dashboard.ngrok.com/
- n8n documentation: https://docs.n8n.io/

## Maintenance
To update containers:
```bash
docker compose pull
docker compose up -d