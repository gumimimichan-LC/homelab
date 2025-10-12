# Raspberry Pi 5 Lab — Overclocking & Performance Testing

**Purpose**  
Learn *"safe"* ARM overclocking, validate system stability under stress, and prepare the Pi for future honeypot experiments.

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
  2. Create a dedicated user for lab experiments (`rasputin`( idk close to raspi))  
  3. Install monitoring and stress-testing tools:
     ```bash
     sudo apt install -y stress-ng htop lm-sensors
     ```
  4. Enable necessary kernel modules and firmware for NVMe hat (if required)

  Optional: I used a monitoring software from [Skatter bencher](https://github.com/SkatterBencher/rpi5-telemetry-python) as it collectively gathered all telemetry using python. In his overclocking video, he using a command to execute and start it but i always found just going to the file and opening it with the python editor raspios comes with and just running it.

---

## Overclocking Achievements & Strategy
- **CPU frequency achieved:** 3.2 GHz  
- **GPU frequency achieved:** 1.1 GHz
- **Avg. GPU Voltage:** 0.89V
- **Temperatures:** consistently under 50°C under full load  
- **Observations:** out-of-the-box performance allowed extreme overclocking with full stability while running `stress-ng` and `Geekbench`. Idle temps sub 30°C.  

**Notes on approach:**  
- Incremental overclocking: increase CPU/GPU frequencies in small steps, stress test each increment
- Backup SD card or NVMe image before making changes (using `dd` or Raspberry Pi Imager).  
- Monitor temps constantly with `vcgencmd measure_temp` and `htop`.  

---

## Stress-Testing & Monitoring
- **Stress test command example:**
  ```bash
  stress-ng --cpu 0 --timeout 600s

## Notes
- I recommend increasing mV by 25 to be safe but it cant go above 1V stock unless you flash the bios.
- The CPU Clock speed is capped at 3GHz on older models but some newer models have allowed 3+GHz stock, such as mine. Otherwise you'd have to change settings to allow that.
- Stress-ng has a like all command which hits everything on the pi at once but in my testing it would just brick it. I just recommend making sure its stable in the overclock since with the cooler I have it was impossible to get it above 50c for more than 20 seconds.
