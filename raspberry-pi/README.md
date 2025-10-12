# Raspberry Pi 5 Lab — Overclocking & Performance Testing

**Purpose**  
Learn *"safe"* ARM overclocking, validate system stability under stress, and prepare the Pi for future honeypot experiments.  
*(I was prepared to kill this Pi.)*

---

## Hardware & Peripherals
- **Model:** Raspberry Pi 5, 16GB RAM  
- **Cooling:** Argon 60mm active cooler  
- **Power:** Official Raspberry Pi PSU  
- **Storage:** 1TB Crucial NVMe SSD on Pi Hat (bottom)  

---

## OS & Base Setup
- **Operating System:** Raspberry Pi OS (64-bit)  
- **Base steps:**
  1. Full system update:
     ```bash
     sudo apt update && sudo apt full-upgrade -y
     ```
  2. Create a dedicated user for lab experiments (`rasputin` — idk close to raspi)  
  3. Install monitoring and stress-testing tools:
     ```bash
     sudo apt install -y stress-ng htop lm-sensors
     ```
  4. Enable necessary kernel modules and firmware for NVMe hat (if required).

Optional: I used a monitoring software from [SkatterBencher](https://github.com/SkatterBencher/rpi5-telemetry-python) as it collectively gathered all telemetry using Python.  
In his overclocking video, he used a command to execute and start it, but I always found just going to the file, opening it with the Python editor that Raspberry Pi OS comes with, and running it was easier.

---

## Overclocking Achievements & Strategy
- **CPU frequency achieved:** 3.2 GHz  
- **GPU frequency achieved:** 1.1 GHz  
- **Avg. Core Voltage:** 0.89V  
- **Temperatures:** consistently under 50°C under full load  
- **Observations:** out-of-the-box performance allowed extreme overclocking with full stability while running `stress-ng` and `Geekbench`. Idle temps sub 30°C.  

## Stress-Testing & Monitoring
- **Stress test command example:**
  ```bash
  stress-ng --cpu 0 --timeout 600s

**Notes on approach:**  
- Incremental overclocking: increase CPU/GPU frequencies in small steps, stress test each increment.  
- Backup SD card or NVMe image before making changes (using `dd` or Raspberry Pi Imager`).  
- Monitor temps constantly with `vcgencmd measure_temp` and `htop`, or use SkatterBencher’s telemetry monitor.  

---

## Final Notes
- I recommend increasing mV by 25 to be safe, but it can’t go above 1V stock unless you flash the BIOS. (dangerous)
- The CPU clock speed is capped at 3GHz on older models, but some newer models have allowed 3+GHz stock (like mine). Otherwise, you'd have to change settings to allow that.  
- `stress-ng` has an “--all” command that hits everything on the Pi at once, but in my testing it would just brick it.  
- I just recommend making sure it’s stable in the overclock since with the cooler I have, it was impossible to get it above 50°C for more than 20 seconds.  
- My Raspberry Pi is extremely lucky for out-of-the-box performance — ran sub-30°C idle and easily overclocked to 3.2GHz without any crashing while running `stress-ng` and `Geekbench`. Still couldn’t watch 1080p videos.
- The cooler came with thermal pads. In installation videos (which are rare), many people only applied one pad to the PMIC chip. I installed them on the PMIC, RAM, and I/O chip, and used a PTM7950 Phase Change Thermal Pad on the cpu from my previous 5900X tuning attempt (where I was temp-limited on air cooling). This likely helped maintain such low operating temperatures during stress tests.


