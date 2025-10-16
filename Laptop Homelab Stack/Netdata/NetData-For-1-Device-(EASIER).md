# Netdata — Real-Time System & Network Monitoring

# DISCLAIMER
YOU CANNOT ADD SERVICES USING THIS GUIDE. FOLLOW THE OTHER IF YOU DESIRE TO ADD SERVICES.

## Purpose
- Provides real-time performance and health monitoring for your system, services, and applications.  
- Ideal for tracking CPU, memory, disk, network, and process activity in an interactive web dashboard.  
- Helps identify bottlenecks, anomalies, and resource spikes at a glance with minimal setup.  

---

## OS & Environment
- **Host:** Laptop (Linux-based)  
- **Install Type:** Native (system package, not containerized)  
- **Integration:** Used to monitor Pi-hole, Unbound, and system performance metrics  

---

# Netdata Installation & Configuration

## 1. Install Netdata
```bash
sudo apt update
sudo apt install netdata -y
```
Still using sudo apt update

---

## 2. Enable and Start the Service
```bash
sudo systemctl enable netdata
sudo systemctl start netdata
sudo systemctl status netdata
```
Should show active (running) after the last command

## 3. Access the Dashboard

Netdata runs a local web interface on port **19999** by default

# OPTIONAL:
I RDP into my laptop to access the thing since it's so trash. It's also mashed behind 50 tangled cables so it's annoying to sit on the floor and mess with it. In order to be able to access the web interface on another device you must enable it to listen on each interface.

1. Open the config menu
```yaml
sudo nano /etc/netdata/netdata.conf
```
2. Edit the "Bind socket to IP"
   1. Scroll down to [global]
   2. Change 127.0.0.1 (loopback) to 0.0.0.0
   3. Ctrl+O, Enter, then Ctrl+X
3. Use the command:
   ```bash
   sudo systemctl restart netdata
   ```
4. Check firewall for port 19999:
   ```bash
   sudo ufw allow 19999/tcp
   ```
5. Profit.
   Now it should be accessible from all interfaces and be listening
   Also TCP port 19999 was already open for me but it doesn't hurt to make sure prior

- Open your browser and go to:  
  - http://127.0.0.1:19999 - for if you're on your host device 
  - http://IP-of-host-device:19999 - if just on the same network

# Networking & Ports

| Port   | Protocol | Description                 |
|--------|----------|-----------------------------|
| 19999  | TCP      | Netdata local web dashboard |

# Security / Hardening

- Runs locally — not publicly exposed by default
- Minimal overhead: lightweight and efficient

# Integration with Pi-hole & Unbound

- Monitor Pi-hole DNS queries, block rates, and network activity in real time 
- Track Unbound performance (queries per second, latency, cache hit rates) using the **unbound collector**  
- Useful for diagnostics: quickly identify spikes in blocked domains or DNS latency
