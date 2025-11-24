# Installation Guide

Complete step-by-step installation instructions for YouTrack on Alpine Linux.

## Prerequisites

- Proxmox VE environment
- Alpine Linux VM (2 vCPU, 2GB RAM, 20GB storage)
- Basic Linux command line knowledge

## Step 1: Alpine Linux VM Setup

### Create VM in Proxmox
1. Download Alpine Linux ISO
2. Create VM with specifications above
3. Install Alpine Linux (standard installation)

### Initial System Configuration
```bash
# Update system
apk update && apk upgrade

# Install required packages
apk add docker docker-compose curl nano openjdk11
```

## Step 2: Docker Configuration
```bash
# Enable Docker at boot
rc-update add docker boot

# Start Docker
service docker start

# Verify installation
docker --version
docker-compose --version
```

## Step 3: Directory Structure
```bash
# Create application directory
mkdir -p /opt/youtrack/{data,conf,logs,backups}

# Set proper ownership (YouTrack runs as UID 13001)
chown -R 13001:13001 /opt/youtrack/data
chown -R 13001:13001 /opt/youtrack/conf
chown -R 13001:13001 /opt/youtrack/logs
chown -R 13001:13001 /opt/youtrack/backups
```

## Step 4: TLS Certificate Generation
```bash
# Navigate to config directory
cd /opt/youtrack/conf
mkdir -p certs

# Generate self-signed certificate
keytool -genkey -alias youtrack \
  -keyalg RSA -keysize 2048 \
  -validity 365 \
  -keystore certs/youtrack.jks \
  -storepass changeit \
  -keypass changeit \
  -dname "CN=youtrack.local, OU=IT, O=HomeLab, L=City, ST=State, C=US"

# Set permissions
chown 13001:13001 certs/youtrack.jks
chmod 600 certs/youtrack.jks
```

## Step 5: Docker Compose Configuration

Create `/opt/youtrack/docker-compose.yml`:
```yaml
version: '3.8'

services:
  youtrack:
    image: jetbrains/youtrack:2025.3.108480
    container_name: youtrack-server
    ports:
      - "8080:8080"
      - "8443:8443"
    volumes:
      - /opt/youtrack/data:/opt/youtrack/data
      - /opt/youtrack/conf:/opt/youtrack/conf
      - /opt/youtrack/logs:/opt/youtrack/logs
      - /opt/youtrack/backups:/opt/youtrack/backups
    restart: unless-stopped
    environment:
      - TZ=America/Los_Angeles
      - YOUTRACK_JVM_OPTS=-Djetbrains.youtrack.ssl.keyStore=/opt/youtrack/conf/certs/youtrack.jks -Djetbrains.youtrack.ssl.keyStorePassword=changeit -Djetbrains.youtrack.baseUrl=https://youtrack.local:8443
```

## Step 6: Deploy YouTrack
```bash
cd /opt/youtrack
docker-compose up -d

# Check logs
docker-compose logs -f
```

## Step 7: Initial Setup

1. Access `https://YOUR_IP:8443` in browser
2. Accept self-signed certificate warning
3. Complete setup wizard
4. Create admin account
5. Configure base URL

## Step 8: Tailscale Setup (Optional)
```bash
# Install Tailscale
apk add tailscale

# Enable and start
rc-update add tailscale
rc-service tailscale start

# Authenticate
tailscale up --accept-routes --ssh

# Get Tailscale IP
tailscale ip -4
```

## Verification
```bash
# Check container status
docker-compose ps

# Test local access
curl -k https://localhost:8443

# Check logs for errors
docker-compose logs youtrack | grep -i error
```

## Next Steps

- [Configuration Guide](configuration.md)
- [Backup Setup](../scripts/backup.sh)
