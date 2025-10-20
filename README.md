# Home Lab Overview

This is my personal **Cybersecurity & systems homelab** repository.
Everything I build and set up will be **free and self-hosted**, so it's accessible to others without paywalls or subscriptions.
The focus is on **learning, monitoring, and documenting real-world setups**.

---

## Current Projects

- [Laptop Homelab Stack](./Laptop%20Homelab%20Stack/README.md)
  (this is what im currently loading up with everything I can)

---

## Finished Projects

- [Plex Media Server](./plex-server/README.md)
- [Raspberry Pi building/testing](./raspberry-pi/README.md)

---

## Planned Projects

- [Planned]Router DMZ + network isolation
- [Planned] T-Pot honeypot

---

## Goals
- Gain hands-on cybersecurity experience
- Practice system administration & monitoring
- Build a "professional" homelab portfolio *(hopefully)*

---

## Environment
- **Hardware:**
  - Raspberry Pi
  - Personal PC
  - Home server (Plex, etc.)
  - Laptop
  - Backup PC
  
- **Operating Systems:**
  - Linux (Ubuntu / Raspberry Pi OS)
  - Windows 11
  
- **Network Topology:**
  - ISP Router (main router)  
    - Backup PC (wired)  
    - 2.5G Network Switch
      - Personal PC (wired) 
      - Home Server (wired)
      - Laptop (wired)
      - Tenda Router (main Wi-Fi + LAN)  
        - Linksys Router (DMZ)  
          - Raspberry Pi (wired - T-Pot honeypot)
            
---

## **Hardware For each node** 
Wanted To List Everything in my homelab as idk maybe you can know what the limits are based on my hardware.

### DISCLAIMER
Do note that I say MT/s and not Mhz. Ram companies have been basically scamming people by confusing Megatransfers per second compared to Megahertz due to how ram works. Ram is **DDR** which stands for **Double Data Rate** meaning that it transfers data **TWICE** per clock cycle. So my *"3200Mhz"* ram is actually 1600Mhz but due to it being DDR, the ram is actually 3200MT/s. This was a big misconception until DDR5 came out and they started putting 6000Mhz which is insane. So please don't be dumb like a lot of people and confuse the two. It is **NOT** the same.

- Backup PC: Some dell optiplex, Ill check later

- Personal PC:
  - CPU: R9 5900x
  - GPU: RTX 4070 OC
  - RAM: 32GB 3200MT/s

- Home Server
  - CPU: R5 3600x
  - GPU: RTX 2060 Super
  - RAM: 16 GB 3200MT/s

- Laptop - HP Stream 2014
  - CPU: Intel Celeron N3060
  - GPU: Integrated Intel HD Graphics 400
  - RAM: 4 GB DDR3L 1600MT/s

- Raspberry Pi 5 16GB
  - Its a raspberry pi 5 :|
  - HAB nVME 1TB



- **Notes:**
  - To be honest, I have no clue what I'm doing. I am just writing and saying what I've done in the confines of these 4 walls. 
  - Also I am adding a bit of personality to stuff because while I want to show it off later, *currently* it's not for a company, it is to document my findings, projects, and other things.
  - It's serious but not that serious right now. Some personality will show how I truly felt in the moment rather than stating "This inquisitively frustrated me!" no it did not. It made me want to do dispicable acts to the hardware in my room. 
  - Sometimes tech is a chore, sometimes its not. Same goes for learning.

