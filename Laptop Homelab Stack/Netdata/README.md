# Netdata — Real-Time System & Network Monitoring

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

- Open your browser and go to:  
  - http://127.0.0.1:19999 - for if you're on your host device 
  - http://<IP-of-host-device>:19999 - if just on the same network

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
