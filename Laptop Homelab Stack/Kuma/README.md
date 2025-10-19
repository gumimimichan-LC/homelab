# Uptime Kuma — Self-Hosted Status Monitoring

## Purpose
- Monitors **websites, services, and endpoints** for uptime/downtime.  
- Sends **alerts** via multiple notification methods when something goes down.  

---

## OS & Environment
- **Host:** Laptop (Linux-based) or server  
- **Install Type:** Bare Metal  
- **Integration:** Can monitor services like Pi-hole, Unbound, home lab devices, and web apps  

---

# Uptime Kuma Installation & Configuration

## Installation Steps

### 1. Install Dependencies
```bash
sudo apt update
sudo apt install git curl -y
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install nodejs -y
```

### 2. Check it's Installed
```bash
node -v
npm -v
```

### 3. Download Uptime Kuma
```bash
cd /opt
sudo git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
sudo npm run setup
```

### 4. Run it Manually
```bash
node server/server.js
```
Go to http://localhost:3001 to start the setup

### 5. Create a systemd service
```bash
sudo nano /etc/systemd/system/uptime-kuma.service
```
Paste this
```yaml
[Unit]
Description=Uptime Kuma
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/opt/uptime-kuma
ExecStart=/usr/bin/node server/server.js
Restart=always
Environment=NODE_ENV=production
# Optional: adjust memory or port if needed

[Install]
WantedBy=multi-user.target
```
Save and exit (CTRL+O, Enter, CTRL+X)
Then run:
```bash
sudo systemctl daemon-reload
sudo systemctl enable --now uptime-kuma
```

### 6. Verify it's running
```bash
sudo systemctl status uptime-kuma
```
Then open:
```bash
http://127.0.0.1:3001
```
### 7. Add monitors

I'm gonna keep this simple, I'm only gonna explain unbound as an example.

Type: TCP port
Frienly Name: (can be whatever but) Unbound
Hostname: 127.0.0.1
Port: 5335
Monitoring Group: Laptop Stack (keeps it simple and organized)
Description: Unbound - DNS Cache Server/Recursive DNS Lookup
Save.

Notes:
- Pretty simple is kinda nice
- Not all programs are easy but if you think outside the box you can make anything work - Ex. pihole was confusing but i just linked the web ui and it worked











