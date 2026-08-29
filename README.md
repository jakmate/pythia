# Homelab Server Documentation

---

# Server Overview

| Item              | Value                                       |
| ----------------- | ------------------------------------------- |
| Hostname          | `delphi`                                    |
| Purpose           | Media Streaming + Photo Backup + Scrobbling |
| OS                | Debian 13 'trixie'                          |
| Container Runtime | Docker + Docker Compose                     |
| Remote Access     | Tailscale VPN                               |
| SSH Access        | Enabled via Tailscale                       |

---

# Hardware Specifications

## System

| Component | Details        |
| --------- | -------------- |
| CPU       | Intel i3-6100u |
| RAM       | 8GB DDR4       |
| Storage   | 400GB          |
| Network   | WiFi           |

---

# Installed Packages

## Base Utilities

```bash
curl
wget
git
unattended-upgrades
rsync
```

## Monitoring

```bash
btop
powertop
smartmontools
```

## Networking

```bash
openssh-server
tailscale
ufw
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
│   ├── audiomuse-ai/
│   │   ├── docker-compose.yml
│   │   └── .env
│   │
│   ├── explo/
│   │   ├── docker-compose.yml
│   │   └── .env
│   │
│   ├── immich/
│   │   ├── docker-compose.yml
│   │   ├── .env
│   │   └── postgres/
│   │
│   ├── maloja/
│   │   ├── docker-compose.yml
│   │   └── data/
│   │
│   ├── multi-scrobbler/
│   │   ├── docker-compose.yml
│   │   └── data/
│   │
│   └── navidrome/
│       ├── docker-compose.yml
│       └── data/
│
└── data/
    ├── music/
    │   └── Artist/
    │       └── Album/
    │
    └── library/
```

---

# Docker Management

## Docker Containers

| Container       | Purpose                        | Port  |
| --------------- | ------------------------------ | ------|
| Navidrome       | Music Streaming Server         | 4533  |
| Immich          | Photo & Video Backup           | 2283  |
| Audiomuse AI    | Music Discovery / AI           | 8000  |
| Maloja          | Scrobbling / Listening History | 42010 |
| Multi Scrobbler | Scrobbling Aggregation         | 9078 |
| Explo           | Media / Music Service          | 7288 |

> **Note:** Ports for Multi Scrobbler and Explo are intentionally not documented here. Refer to their respective `docker-compose.yml` files for the current port configuration.

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
docker logs audiomuse_ai
docker logs maloja
docker logs multi-scrobbler
docker logs explo
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

* major version upgrades
* non-security packages
* troubleshooting dependency issues

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

* [ ] Remove audiomuse ai port access for database and AI
* [ ] Connection back to PC (Samba?)
* [ ] Add monitoring
* [ ] Harden SSH
* [ ] Implement backups
* [ ] Define restore procedure
* [ ] Replace single drive with RAID or NAS

---

# Change Log

| Date       | Change                                                                       |
| ---------- | ---------------------------------------------------------------------------- |
| 2026-05-18 | Initial documentation created                                                |
| 2026-05-20 | Powertop `--auto-tune` service added                                         |
| 2026-05-22 | Edit `/etc/default/grub` to turn off display after 5 minutes                 |
| 2026-05-22 | Add UFW                                                                      |
| 2026-05-27 | Add updating of Docker images via service + timer                            |
| 2026-05-29 | Edit `/etc/default/grub` `pcie_aspm=off`, got rid of error logs from Atheros |
| 2026-05-29 | Disable mic, camera and touchpad in BIOS                                     |
| 2026-05-31 | Enable SMART in BIOS, install smartmontools                                  |
| 2026-06-06 | Add audiomuse-ai container and plugin for Navidrome                          |
| 2026-06-16 | Add rsync                                                                    |
| 2026-08-15 | Add Maloja                                                                   |
| 2026-08-29 | Add Multi Scrobbler and Explo                                                |
