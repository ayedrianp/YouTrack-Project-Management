# YouTrack Project & Task Management System

> Self-hosted containerized issue tracking and project management platform for homelab infrastructure management and personal productivity

![Dashboard](https://github.com/ayedrianp/YouTrack-Project-Management/blob/main/Project%20Folder/Dashboard%20Screenshot.png)

##  Project Overview

Deployed JetBrains YouTrack on Alpine Linux using Docker to create a lightweight centralized system for project tracking, task management, infrastructure maintenance, and incident resolution across my homelab environment. Using Tailscale to access remotely from my devices.

##  Skills Demonstrated

- **Containerization**: Docker, Docker Compose
- **Linux Administration**: Alpine Linux, system services, file permissions
- **Security**:  zero-trust networking (Tailscale) for secure tunneling
- **Infrastructure as Code**: Declarative configuration
- **Project Management**: Agile workflows, sprint planning, issue tracking
- **ITSM**: Incident management, change control, problem tracking

##  Architecture
```
Router
  │
  ├─── Proxmox Host
  │     └── Alpine Linux VM
  │          ├── Docker Engine
  │          └── YouTrack Container
  │               ├── HTTP: <IP ADDR>:8080
  │               └── HTTPS: <IP ADDR>:8443
  │
  └─── Tailscale (Remote Access)
```

##  Current Issues: 
- Port listening not available for 8443 despite enabled in config.
	- Will explore at a later date. Tailscale used for ZT access.  	 


##  Use Cases

### Project Management
- Track homelab infrastructure projects in one tidy space.
- Plan multi-step technical implementations
- Document project progress and outcomes

### Task & Todo Management
- Daily task lists and priorities
- Quick capture for ideas and improvements
- Recurring maintenance schedules
- Long-term goal tracking

### Incident & Problem Tracking
- Log homelab incidents and outages
- Track troubleshooting steps
- Document solutions and root causes
- Build knowledge base

### Infrastructure Maintenance
- Schedule routine maintenance tasks
- Track hardware inventory
- Monitor service health
- Document configuration changes

##  Technology Stack

| Component            | Technology                                |
| -------------------- | ----------------------------------------- |
| **OS**               | Alpine Linux 3.x, For its light footprint |
| **Virtualization**   | Proxmox VE                                |
| **Containerization** | Docker + Docker Compose                   |
| **Application**      | JetBrains YouTrack                        |
| **Security**         | TLS/SSL (JKS), Tailscale VPN              |
| **Ports**            | 8080 (HTTP), 8443 (HTTPS)                 |
| Mesh VPN             | Tailscale                                 |

##  Documentation

- [Installation Guide](docs/installation.md) - Complete setup instructions
- [Configuration Guide](docs/configuration.md) - Workflow and customization
- [Troubleshooting](docs/troubleshooting.md) - Common issues and solutions

##  Screenshots

## Project List

![Projects Screenshot.png](https://github.com/ayedrianp/YouTrack-Project-Management/blob/main/Project%20Folder/Projects%20Screenshot.png)

## Project Knowledge Base

![KB Screenshot](https://github.com/ayedrianp/YouTrack-Project-Management/blob/main/Project%20Folder/KB%20Screenshot.png)
##  Security Features

- Zero-trust remote access via Tailscale
- Container isolation
- Proper file permissions (UID-based)
- Automated backups

##  Key Metrics

- **Deployment Time**: ~30 minutes
- **Resource Usage**: 2 vCPU, 2GB RAM, 20GB storage
- **Projects Tracked**: 5 active boards, 2 back burner
- **Backup Frequency**: Daily automated backups


##  Future Enhancements

- [ ] Email notifications for critical tasks
- [ ] API automation for script-based ticket creation
- [ ] Mobile app integration
- [ ] TLS/SSL certificates

## 📖 Resources

- [YouTrack Documentation](https://www.jetbrains.com/help/youtrack/)
- [Docker Documentation](https://docs.docker.com/)
- [Alpine Linux Wiki](https://wiki.alpinelinux.org/)
- [Tailscale Documentation](https://tailscale.com/kb/)

##  Other Projects

- [Wazuh-Suricata Integration Lab](../wazuh-suricata-integration-lab) - Security monitoring

---

**Environment**: Proxmox VE 8.x | Alpine Linux 3.19+ | Docker 24.x | YouTrack 2025.3
