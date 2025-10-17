# Intro
  I am not leveraging the help of ChatGPT for the final product. I do write the whole thing myself but I have ChatGPT copy it into the format I prefer that I did (with the help of it) the first time.

  I am overly annoyed with the fact I have to do this so this will be as NOT straight foward as possible since my genuine emotions and thoughts will be broadcasted through this medium.

  ---

  ## Purpose
  
  The reason you'd want a parent-child set up is so you can aggregate all the data into one dashboard. I will eventually have a honeypot using TPot on my network but have decided against running data to the dashboard as it could compromise my network. Tis will be covered in the Honeypot when I finally get TWO more ethernets to hook it all up. I also installed the basic version on the other one so you can't add services. Awesome. Let me go fix that right now so people know.

  TLDR: Parent-Child configuration is good for when you have multiple devices running services you want to monitor 

  ---

  ## Installation

1. Uninstalling
  
  To keep it simple just gonna do a bash and copy it all

  ```bash
sudo systemctl stop netdata
sudo apt remove --purge netdata -y
sudo rm -rf /etc/netdata /var/lib/netdata /usr/lib/netdata /usr/libexec/netdata

  ```
    1. Stop the Netdata service
    2. Remove the minimal package completely
    3. Clean up leftover files and directories

2. Install the whole stupid thing
   ```bash
    bash <(curl -Ss https://raw.githubusercontent.com/netdata/netdata/master/packaging/installer/kickstart.sh) --stable-channel
   ```
   Will now install all plugins: go.d.plugin, python.d.plugin, charts.d.plugin, etc.
   Allows integration...Great.

3. Verify install because at this point, I will not be redoing this again.
   ```bash
  ls /usr/libexec/netdata/go.d/
    ```
  Hopefully you see an output
