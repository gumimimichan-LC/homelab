# Preface

I wanted to include this device in the home network as nowadays E-Waste is a massive issue. Showing how to repurpose a laptop that can't even run windows 10 (it did but had 100MB of ram to spare after all updates) I believe is important so others on a budget can still gain the necessary knowledge to do what I have set out to do as well as reduce the amount of E-Waste. I hope to demonstrate how old hardware can be used as a learning tool and can make homelab setups affordable and practical for anyone interested. (Fun Fact: I genuinely used this device in 4th/5th grade. It ran Animal Jam and Roblox just fine, they were all the rage at this time.)

# Laptop Homelab Stack

This folder contains the services that run on my old HP Stream laptop from around 2014. 
Like everything else, it is all free, self hosted, and focused on **network management, monitoring, and learning cybersecurity**.

---

## Services
These are the services I plan to run:

- [Pi-hole](./Pi-hole/README.md) — DNS filtering and ad-blocking for my home network.  
- [Unbound](./unbound/README.md) — Recursive DNS resolver to improve privacy and DNS speed.  
- [Uptime Kuma](./Kuma/README.md) — 
- [Netdata](./Netdata/README.md) — Real-time system and network monitoring.

---

## Notes
- All services run on the bare metal OS (Ubuntu) since 2/4 interact directly with networking.  
- Main use is learning so services that affect the network will be deployed on my network, my room. Not the whole network. (looking back i dont know what i was trying to say here)
- See each folder for *"detailed setup"*, configuration, and observations.
