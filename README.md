# Homelab Server Documentation

---

# Server Overview

| Item | Value |
|---|---|
| Hostname | `delphi` |
| Purpose | Media Streaming + Photo Backup |
| OS | Debian 13 'trixie' |
| Container Runtime | Docker + Docker Compose |
| Remote Access | Tailscale VPN |
| SSH Access | Enabled (LAN + Tailscale) |

---

# Hardware Specifications

## System

| Component | Details |
|---|---|
| CPU | Intel i3-6100u |
| RAM | 8GB DDR4 |
| Storage | 400GB |
| Network | WiFi |

---

# Installed Packages

## Base Utilities

```bash
curl
wget
git
btop
unattended-upgrades
```

## Networking

```bash
openssh-server
tailscale
```

---

## Containers

```bash
docker
docker-compose
```

---

# File Structure

```text
/
├── containers/
│   ├── immich/
│   │   ├── docker-compose.yml
│   │   ├── .env
│   │   └── postgres/
│   │
│   └── navidrome/
│       ├── docker-compose.yml
│       └── data/
│
└── data/
    ├── music/
    │   └── Artists/
    │
    └── library/
```

---

# Docker Management

## Docker Containers

| Container | Purpose | Port |
|---|---|---|
| Navidrome | Music Streaming Server | 4533 |
| Immich | Photo & Video Backup | 2283 |

## Start Services

```bash
docker compose up -d
```

## Stop Services

```bash
docker compose down -v
```

## Update Containers

```bash
docker compose pull
docker compose up -d
```

## View Running Containers

```bash
docker ps
```

## View Logs

```bash
docker logs immich_server
docker logs navidrome
```

---

# Tailscale Management

## Check status

```bash
tailscale status
```

## Get server IP

```bash
tailscale ip -4
```

---

# Maintenance

## System Updates

Security updates are handled automatically via unattended-upgrades.

Manual updates are only needed for:
- major version upgrades
- non-security packages
- troubleshooting dependency issues

### Manual update (if required)

```bash
sudo apt update && sudo apt upgrade -y
```

## Check Docker Containers

```bash
docker ps
```

## Restart Services

```bash
sudo systemctl restart docker
```

---

# Monitoring Commands

## Hardware

```bash
btop
```

## Disk Usage

```bash
df -h
```

## Memory Usage

```bash
free -h
```

## Running Services

```bash
systemctl list-units --type=service
```

---

# TODO

- [ ] Connection back to PC
- [ ] Add monitoring
- [ ] Harden
- [ ] Implement backups
- [ ] Define restore procedure
- [ ] Replace single drive with RAID or NAS
- [ ] Optimize power consumption

---

# Change Log

| Date | Change |
|---|---|
| 2026-05-18 | Initial documentation created |
