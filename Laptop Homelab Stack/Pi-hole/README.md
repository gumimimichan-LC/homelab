
# Laptop Pi-hole Lab — DNS Filtering & Ad-blocking

**Purpose**  
Filter DNS requests and enable network-wide ad-blocking for my home network.  
*(Main goal: block ads and trackers while learning Pi-hole setup and DNS management.)*

---

## Hardware & Environment
- **Device:** 2014 HP Stream Laptop  
- **Storage:** 256 GB microSD  
- **Power:** Laptop running on charger, battery removed  
- **Networking:** Ethernet preferred (static IP assigned)  
- **Installation Type:** Native Ubuntu (not Dockerized)  

---

## OS & Base Setup
- **Operating System:** Ubuntu  
- **Base steps:**
  1. Full system update:
     ```bash
     sudo apt update && sudo apt upgrade -y
     ```
  2. Assign static IP via **Settings → Network → IPv4 → Manual** (copied existing IP, gateway, and subnet).  
  3. Prevent sleep when lid is closed:
     ```bash
     sudo nano /etc/systemd/logind.conf
     ```
     - Change:
       ```
       #HandleLidSwitch=suspend
       ```
       to:
       ```
       HandleLidSwitch=ignore
       ```
     - Apply changes:
       ```bash
       sudo systemctl restart systemd-logind
       ```

---

## Pi-hole Installation & Configuration
- Install Pi-hole:
  ```bash
  curl -sSL https://install.pi-hole.net | bash
- **Blocklists used:** StevenBlack’s Unified Hosts  
- **Upstream DNS:** Quad9 (filtered, DNSSEC, ECS)  
- **Privacy Level:** Level 2 (hide domains & clients)  
- **Query Logging:** Disabled  

---

## Networking & Ports

- **Web Interface Port:** 80  
- **Static IP:** Required for reliable DNS resolution  
- **Exposure:** Local network only (do not expose to WAN)  

---

## Security & Hardening

- Optional: enable Anonymous Mode to further reduce logging  
- Avoid exposing Pi-hole to the internet  

---

## Monitoring & Logging

- Pi-hole web UI provides effective, real-time query stats  
- does show your computer stats (like task manager)

---

## Notes

- I like their Pi-hole Midnight theme but the star trek one felt like there was too much going on.
- setup was quite straight foward and GUI is easy to learn
- PLEASE when doing the laptop always on, do NOT be like me and try to break everything because its not working since you forgot to remove the # from the line of code. It will save you a lot of happiness and keep anger away.
---

## what I Learned

- Learned DNS-level ad-blocking for the entire network  
- Became familiar with Ubuntu networking and service management  

**Next Improvements:**
- Add Unbound for recursive DNS resolution  
- Integrate Uptime Kuma for service health monitoring  
- Expand monitoring with Netdata dashboards


  
