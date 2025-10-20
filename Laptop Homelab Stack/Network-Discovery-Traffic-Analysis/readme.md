# Nmap + Tcpdump + Wireshark

Purpose
Learn to scan, map, and analyze my own network traffic to understand how devices communicate, how DNS resolution works, and how packets move across my local network.
Really I just combined these 3 since I've heard about all of them but don't actually know how they work so today is the day.
---
## Hardware & Environment
- Same laptop as normal, I mean its under the same category man.
- Ethernet preferred, static IP set manually
- we do NOT do docker.
---
## OS & Base Setup

OS: Ubuntu

### Base steps:

1. UPDATE THAT SYSTEM!
```bash
sudo apt update && sudo apt upgrade -y
```
2. Install what we want
```bash
sudo apt install nmap tcpdump wireshark -y
```
3. Add user to the wireshark group so we don't have to use sudo
```bash
sudo usermod -aG wireshark $USER
```
4. REBOOT!
now you can just you know reboot but it makes rdping into the laptop funky and I have to go and open it and so using the following command you can do it without actually rebooting. We basically just give it a new login shell for the user.
```bash
su - $USER
```
---
## Tools & Configuration
These were just examples I found, if you need the actual command structures just look it up tbh                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             

### Nmap — Network Discovery
Now we do some Nmap-ing!
- Scan devices and detect open ports:
```bash
sudo nmap -sn 192.168.254.0/24
```
-Check what services are running:
```bash 
sudo nmap -sS -sV -O 192.168.254.107
```

### Tcpdump — Raw Packet Capture

- Capture live DNS traffic from Pi-hole/Unbound:
```bash
sudo tcpdump -i any port 53 -vvv
```
- Save a packet capture for later analysis:
```bash
sudo tcpdump -i eth0 -w capture.pcap
```

### Wireshark — Deep Packet Analysis

So unlike the other two, wireshark has a GUI. Since it only watches traffic that the device receives, we will be able to watch pi-hole filtering and DNS recursion by unbound in real time.
Examples for filters for like:
1. DNS - DNS queries obviously
2. ip.addr == 192.168.x.x - that specific IP traffic only
3. tcp.analysis.flags - shows tcp retransmissions or dropped packets

---

### Networking & Ports

#### Scope: Local LAN only — not used for any external scanning or internet targeting.

#### Common Ports Used:
DNS → 53
HTTP → 80
HTTPS → 443

#### Capture Interfaces:
Wi-Fi Ethernet, depending on what you want to inspect.

---

### Ethics:
Now you can do a lot with NMap and wireshark like:

- scanning traffic on unauthorized networks, basically looking at unencrypted traffic
- mapping network topology
  
While it's only two things, these things can be used for more malicious things. It's just summarized.

Notes:










