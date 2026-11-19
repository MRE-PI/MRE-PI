---
nav_order: 2
layout: default
title: OS Install
parent: Implementation
nav_enabled: true
---
.
The PI OS install for Raspberry Pi is very simple.  Our goal is to install a Raspberry Pi OS Lite (64-bit) image on each device SD card.

[Download the Raspberry Pi Imager SW for their website](https://www.raspberrypi.com/software/) , install and open.
You will select your device and then Raspberry Pi OS (Other)
Then select Raspberry Pi OS Lite (64-bit)  
Then Customization.  Very routine information but this is the tricky part.  You need the Public Key from your YubiKey to enable SSH Authentication.  The imager makes this very easy.
Raspberry Pi connect is not installed due to the security implications but is a very interesting tool.

Sensor Requirements
===================
The sensor is based on a Raspberry PI Zero 2W  
After PI OS Lite is installed and booted on the device, its only additional requirements are as follows:  

First, a clean update
```markdown
sudo apt update && sudo apt full-upgrade -y
```
and second,
```markdown
sudo apt remove rpicam-apps-lite
```
```markdown
sudo apt install ffmpeg rpicam-apps
```
ffmpeg is not a small install  

### Create the streaming service  
```markdown
sudo nano streamslow.sh
```
```markdown
#!/bin/bash
nice -n -19 rpicam-vid -t 0s --width 1456 --height 1088 \
--vflip --nopreview 1 --low-latency 1 --hdr off --flush 1 \
--buffer-count 6 --exposure normal --sharpness 1.1 --contrast 1.2 \
--brightness 0.0 --saturation 1.0 --ev +1.0 --awb auto \
--profile high --level 4.2 --codec libav --libav-format flv \
-n --framerate 5 -b 1550000 --autofocus-mode default --autofocus-range macro \
--denoise auto --inline -g 60 \
-o "rtmp://192.168.12.12/pi/PiCam2W05"
```
```markdown
sudo chmod 755 /home/fox-admin/streamslow.sh
```
For AI Camera
```markdown
sudo apt install imx500-all
```
### Create Service
```markdown  
sudo nano /etc/systemd/system/streamslow.service  
```
```markdown
[Unit]  
Description=Start Camera Script  
After=multi-user.target  
[Service]  
ExecStart=/home/fox-admin/streamslow.sh  
Type=idle  
[Install]  
WantedBy=multi-user.target  
```

```markdown
sudo chmod 644 /etc/systemd/system/streamslow.service
```
Finally, tell systemd to run it at boot:
```markdown
sudo systemctl enable streamslow.service
```
```markdown
sudo systemctl start streamslow.service
```
```markdown
sudo systemctl restart streamslow.service  
```

Once completed the sensor device can proceed to [OS Hardening](https://mre-pi.com/STIG/OS%20Hardening.html)  

Edge Server Requirements  
========================  
The Edge Server will require the following  
1. Motion Application  
2. MariaDB Database  
3. NGINX Web Server  
4. Supporting Video Libraries
   
