# Plex Media Server & Media Management Suite

**Purpose**  
Host and manage personal media (movies, TV shows, music, books) on my home network, while also integrating automated tools for media acquisition and organization.

---

## Quick Summary
- **Host machine:** `coolbeansdude` (Windows 11)  
- **OS:** Windows 11  
- **Services running directly:** Plex Media Server, Sonarr, Radarr, FlareSolver, Qbittorent, Mullvad  
- **Services containerized:** Overseerr (Docker)  
- **Access:** LAN-only (no external access configured)  
- **Transcoding:** Hardware-accelerated via GPU (if available) / fallback to software  

---

## Installation & Setup
1. **Install Plex Media Server** directly on Windows 11.  
2. **Install Sonarr and Radarr** for automated media management and downloads.  
3. **Install FlareSolverr** to bypass site restrictions for Sonarr/Radarr where needed.  
4. **Set up Overseerr** in Docker for managing media requests.  
5. Add libraries in Plex pointing to your media folders.  
6. Configure backups and monitoring (Windows task scheduler or external scripts) to ensure stability.

- The reason I didn't put any other things in docker is because I experienced instability and GPU Passthrough causes glitches in my system. I also had a HV issue at this time which affected AMD's PPM.
---

## More In-depth Setup

I need to look back and redo it to make this decent so ill fix this later

## Networking & Access
- LAN IP: I am not giving you my ips even private 
- Ports used:
  - Plex: TCP 32400
  - Sonarr: 8989
  - Radarr: 7878
  - Overseerr (Docker): 5055
- No external access enabled; all services are internal to home network.

---

## Security & Hardening
- Run all non-Docker services under a dedicated Windows account with limited permissions.  
- Use Windows Firewall to restrict access to local network only.  
- Keep all software updated regularly to avoid security vulnerabilities.  
- No remote access, so exposure to external threats is minimized.

---

## Backup & Maintenance
- Media backups scheduled using Parity 4tb nVME drives.  
- Plex config stored in `%LOCALAPPDATA%\Plex Media Server\` — backup periodically.  
- Monitor Windows stability and service uptime; address any crashes or resource issues.

---

## Monitoring & Logs
- Plex logs: `%LOCALAPPDATA%\Plex Media Server\Logs\`  
- Overseerr logs: Docker logs (`docker logs overseerr`)  
- Optional: Use Resource Monitor or Task Manager to watch CPU, memory, and GPU usage.  
- Observed issue: Windows stability affected media server uptime (not Plex itself).  

---

## What I Learned
- Setting up Plex and supporting services was straightforward.  
- Stability of the host OS can impact uptime of all media services.  
- Running Overseerr in Docker alongside Windows-native services is a clean way to separate environments. (really just ran overseerr in docker due to issues and to learn how docker works on a basic level)

---

## Next Improvements
- Add HTTPS reverse proxy for optional secure external access.  
- Automate backups of Plex and media databases.  
- Monitor service resource usage with Grafana/Prometheus or Windows Task Scheduler notifications.
