---
nav_order: 12
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

