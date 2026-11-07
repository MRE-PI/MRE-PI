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
Its only additional requirements are as follows:  
A clean update
```markdown
sudo apt update && sudo apt full-upgrade -y
```
and 
```markdown
sudo apt install ffmpeg
```


Edge Server Requirements
========================
The Edge Server will require the following  
1. Motion Application  
2. MariaDB Database  
3. NGINX Web Server  
4. Supporting Video Libraries
   
