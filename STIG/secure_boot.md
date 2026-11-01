---
nav_order: 5
layout: default
title: Secure Boot
parent: OS Hardening
nav_enabled: true
---

Raspberry Pi Zero 2 W Secure Boot Provisioning  
===============================================
The Raspberry Pi Zero 2 W cannot be provisioned for secure boot because it lacks the required hardware (EEPROM and secure boot firmware) and is explicitly unsupported by the official Secure Boot Provisioner 

### Why it’s not possible
The Raspberry Pi Zero 2 W’s design does not include the EEPROM and secure boot firmware found in Pi 4‑family and Pi 5‑family boards  

. Secure boot on Raspberry Pi devices relies on:  

A boot ROM with a built‑in public key  

EEPROM storage for storing trusted keys and firmware updates  

Firmware that can verify and load signed OS images  

### The Zero 2 W only supports:

FDE‑only mode (full‑disk encryption without secure boot)  

Naked mode (no encryption, no secure boot)  

The official rpi‑sb‑provisioner documentation confirms: 

“Secure boot is NOT available on Raspberry Pi Zero 2 W devices… Do NOT use secure‑boot mode with Zero 2 W. It will not work” 

A GitHub issue from the project maintainers also states:  

“The secure boot mechanisms used in Raspberry Pi 4‑family and 5‑family devices… make implementing an identical scheme unviable” for Zero 2 W  

### What you can do instead
If your goal is secure OS deployment without secure boot:  

Use FDE‑only provisioning with the Secure Boot Provisioner to encrypt storage and install a trusted OS image  

For full secure boot, you must use a Pi 4, Pi 5, or a Compute Module 4/5, which have the required hardware 

Recommendation
If you need secure boot, choose a supported hardware platform. For the Zero 2 W, you can still achieve encrypted, trusted OS deployment via FDE‑only mode, but you will not have hardware‑level boot verification 

In short: The Zero 2 W cannot be provisioned for secure boot — it’s a hardware limitation, not a software workaround 

