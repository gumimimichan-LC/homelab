# Unbound — Recursive DNS Resolver

## Purpose
- Acts as a local **recursive DNS resolver** for Pi-hole.  
- Improves **privacy** (no external DNS logging) and **performance** (local caching).  
- Validates **DNSSEC** to ensure data authenticity.

---

## OS & Environment
- **Host:** Laptop (Linux-based)  
- **Install Type:** Native (system package, not containerized)  
- **Integration:** Used as upstream DNS for Pi-hole

---

# Unbound Installation & Configuration for Pi-hole

## Installation Steps

### 1. Install Unbound
  ```bash
  sudo apt update
  sudo apt install unbound -y
  ```
  - get used to the sudo apt update
### 2. Download Root Hints
```bash
wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.root
```
 - I didn't have permission so I added sudo and it worked, ex: sudo wget...
### 3. Configure Unbound
```bash
sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf
```

Paste the following:
```yaml
server:
    verbosity: 0
    interface: 127.0.0.1
    port: 5335
    do-ip4: yes
    do-udp: yes
    do-tcp: yes
    hide-identity: yes
    hide-version: yes
    harden-glue: yes
    harden-dnssec-stripped: yes
    use-caps-for-id: yes
    edns-buffer-size: 1232
    prefetch: yes
    qname-minimisation: yes
    num-threads: 2
    so-rcvbuf: 1m
    auto-trust-anchor-file: "/var/lib/unbound/root.key"
    root-hints: "/var/lib/unbound/root.hints"
    private-address: 192.168.0.0/16
    private-address: 10.0.0.0/8
    private-address: 172.16.0.0/12
    private-address: 127.0.0.0/8
```
I had an issue witht the auto-trust-anchor-file, commenting it out simply fixed it.
### 4. Enable and Start Service
```bash
sudo systemctl enable unbound
sudo systemctl restart unbound
sudo systemctl status unbound
```

### 5. Test DNS
```bash
dig pi-hole.net @127.0.0.1 -p 5335
```
```yaml
Expected output: ;; SERVER: 127.0.0.1#5335(127.0.0.1)
```

---

# Pi-hole Configuration, Networking & Security

## Configure Pi-hole

1. Open Pi-hole Admin → Settings → DNS

<img width="447" height="845" alt="image" src="https://github.com/user-attachments/assets/431d668e-ed69-4a54-a38a-d0a626e07380" />

2. Disable other upstream DNS servers

<img width="431" height="818" alt="image" src="https://github.com/user-attachments/assets/7de0a384-f643-4e5e-9669-b53e3e6f7566" />

```bash
Add: 127.0.0.1#5335
```

Save, then restart FTL:
```bash
sudo systemctl restart pihole-FTL
```
---

## Networking & Ports
- Port: 5335   
- Protocol: TCP/UDP
- Description: Local DNS queries from Pi-hole

---

## Security / Hardening
- Runs locally only (not accessible from internet)
- DNSSEC validation enabled for authenticity (auto trust anchor file is what enables DNSSec but the whole system already had it built in which cause a conflict in the config file. Hence the need to disable it.)
- Hides version info and limits buffer size to prevent attacks, Vulnerabilities spefically in exact versions and DDoS attacks respectively.
- Private address blocking to avoid leaking local domains

---

## Notes
While Pi-hole has been working great and blocking many trackers from my browsers (firefox), Overwolf, and others, you don't really see or feel it doing its job. You only know if you check the server with statisics. 
The moment Unbound was up and running, within minutes I noticed everything STARTED loading faster. Unbound doesn't increase the speed at which a website loads but it does for the initial data transfer. The half second it took off of the initialization was actually noticable and makes you feel like the sites loading faster but rather you are just starting the transfer quicker. I definitely recommend Unbound and have already recommended it to friends.

## Overall homelab Notes:
- I really like yaml for lists of things to paste that go into configs, very colorful.
- I feel like I'm getting better at remembering how things work such as Bolding, Italics, Bash/Yaml
- To make sure the instructions are somewhat clear, I've been replicating everything on a Ubuntu VM on my personal windows device and it has worked perfectly for now. If any issues occur you can like message me or make a complaint or something.






