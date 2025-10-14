# Unbound (Recursive DNS Resolver)

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
  
2. Download Root Hints
```bash
wget -O /var/lib/unbound/root.hints https://www.internic.net/domain/named.root
```

3. Configure Unbound
```bash
sudo nano /etc/unbound/unbound.conf.d/pi-hole.conf
```

Paste the following:
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

4. Enable and Start Service
sudo systemctl enable unbound
sudo systemctl restart unbound
sudo systemctl status unbound

5. Test DNS
dig pi-hole.net @127.0.0.1 -p 5335
Expected output: ;; SERVER: 127.0.0.1#5335(127.0.0.1)

# Pi-hole Configuration, Networking & Security

## Configure Pi-hole

Open Pi-hole Admin → Settings → DNS

Disable other upstream DNS servers

Add: 127.0.0.1#5335

Save, then restart FTL:
sudo systemctl restart pihole-FTL

## Networking & Ports
Port    Protocol    Description
5335    TCP/UDP    Local DNS queries from Pi-hole

## Security / Hardening
- Runs locally only (not accessible externally)
- DNSSEC validation enabled for authenticity
- Hides version info and limits buffer size to prevent attacks
- Private address blocking to avoid leaking local domains








