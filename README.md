# Reverse Proxy Setup with Caddy

This project demonstrates a reverse proxy setup using Caddy server to manage multiple web applications. It includes two separate web applications (`hello-store` and `taida-store`) that are served through Caddy's reverse proxy.

## Project Structure

```
.
├── Caddyfile           # Caddy server configuration
├── docker-compose.yml  # Docker compose configuration
├── hello-store/       # First web application
└── taida-store/       # Second web application
```

## Features

- Multiple web applications running simultaneously
- Automatic HTTPS with Caddy
- Docker containerization
- Local development domains
- Reverse proxy configuration

## Prerequisites

- Docker
- Docker Compose

## Host Configuration

Before starting the services, you need to modify your system's hosts file to map the local domains:

1. Open your hosts file with administrator/root privileges:
   - Linux/Mac: `/etc/hosts`
   - Windows: `C:\Windows\System32\drivers\etc\hosts`

2. Add the following lines:
   ```
   127.0.0.1    hello.localhost
   127.0.0.1    taida.localhost
   ```

## Configuration

### Docker Compose

The project uses Docker Compose to orchestrate the following services:

- `hello`: First web application (accessible at hello.localhost)
- `taida`: Second web application (accessible at taida.localhost)
- `caddy`: Reverse proxy server

### Caddy Configuration

Caddy is configured to:
- Expose admin API on port 2019
- Route traffic to respective services based on domain
- Handle automatic HTTPS certificates
- Manage reverse proxy rules for each service

## Getting Started

1. Clone the repository
2. Start the services:
   ```bash
   docker-compose up -d
   ```
3. Access the applications:
   - Hello Store: http://hello.localhost
   - Taida Store: http://taida.localhost

## Ports

- 80: HTTP
- 443: HTTPS
- 2019: Caddy admin API

## Networks

The project uses a dedicated Docker network (`caddy_network`) for internal communication between services.

## Volumes

- `caddy_data`: Persistent data storage for Caddy
- `caddy_config`: Caddy configuration storage

## Development

Each store application runs on port 5173 within its container and is accessible through the Caddy reverse proxy using the configured domains. 