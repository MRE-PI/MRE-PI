---
nav_order: 1
layout: default
title: Home
nav_enabled: true
---

# Securing a Raspberry Pi to Military Standards  

**What and Why**

War is the realm of uncertainty; three quarters of the factors on which action in war is based are wrapped in a fog of greater or lesser uncertainty. A sensitive and discriminating judgment is called for; a skilled intelligence to scent out the truth.

— Carl von Clausewitz

This project is and was a training exercise to remove the fog from the use of computer assets that do not fit the standard mold of enterprise assets.
What was planned was something that could be scattered in the woods, desert, snow, to gather data yet still meet basic Military Cybersecurity requirements. What: 5 rugged assets Why: Cybersecurity Training

## Project Concept & Requirements:

1. [Follow a simplified Acquisition and Systems Engineering Process](https://www.linkedin.com/pulse/cybersecurity-process-integration-v-model-development-jadhav-dvnpc/)  
2. Focus is on Cybersecurity and not the Platform.  
The platform is tailored for a specific Cybersecurity use case. The goal is securing a Raspberry Pi.  The target operating system is PI OS which is a branch of Debian (as is Ubuntu).  The use case is to secure to military standards which can be significantly different from commercial standards.  The platform architecture has flexibility to become many things, but this project will stay focused on Cybersecurity and not for example the many ways and versions you can install the Motion application.  
3. It should be assumed for this exercise only publicly available communications & encryption will be used. However, there are plenty of examples that can be utilized without the acquisition of a TAClane or Link16 communications.  
4. The platform is to be a real-world platform not a rock sitting in a safe.  

## System Design  

Keep it simple. Sensor --> Server --> Gateway  From a cybersecurity perspective that means Gateway Firewall, STIGS, Scans and PKI (see explanations in the overall project materials).  The non-trivial part is the critical thinking to achieve standard STIG and SCAN security requirements with non-standard solutions that meet System Requirements.  The tricky parts like secure-boot and parts of cryptography will be approached gently as to not create the "rock in a safe".  

## Software / Hardware Design  
**Instantiated requirements**  

### Hardware:  

Video  Camera
:  Video is easily implemented on the entire suite of Raspberry Pi products.  It is in effect a sensor.  It could be substituted with a microphone, a temperature sensor, etc.  For this project qty 3 Raspberry Pi Zero 2W computers were used. I had fun with a variety of cameras & lenses.  They are dedicated to just pulling the data stream to minimize points of failure. (i.e. if you toss a dozen in the battlefield, you are not going to go back around to each of them to reboot or repair.)  The Edge Server is in the same enclave and does all the heavy lifting.  

Edge architecture  
: Communications are always a key architecture requirement for Military, whether mobility, encryption requirements.  To achieve this an Edge Server and Communications Gateway were  architected.  
Edge Server
: Raspberry PI CM5 with NVMe Storage in a hardened enclosure

Communications Gateway
: The architected intent is to have multiple channels of communications to include the myriads of versions of 4G, 5G, StarLink, & WIFI to allow distance vice speed tradeoffs without buying a new Gateway every time.  OpenWRT was selected.  It is not currently a Raspberry Pi but will be secured just the same.

**Asset Inventory**  
Sensors (3)  
Edge Server (1)  
OpenWRT WIFI Router (1)  

[Figure 1](https://robert-brown19.github.io/mre-pi/Figure1.html)   
[Image 1](https://robert-brown19.github.io/mre-pi/Image1.html) 

### Software:  

Motion v5 
: Motion is a program that monitors the signal from video cameras and detects changes in the images.  

NGINX 
: Motion supported Webserver configuration option which after Apache Tomcat is very common  

MariaDB 
: A database supported by Motion selected because it is covered by a published Security Technical Implementation Guide (STIG)  

### Cryptography:  

The Military has significant Cryptography requirements that cannot be addressed in public but there are two very basic requiremnets that can.  

Public Key Encryption
: PKI is a requirement for all government systems.  This project implements the YUBIKey because it can meet military requirements. At this stage of the project, I do not have key-management tools architected because they are generally an enterprise level vice organization level solution.  

Federal Information Processing Standards Publication 140-3 SECURITY REQUIREMENTS FOR CRYPTOGRAPHIC MODULES. 
: FIPS 140-3 Implementation will not be addressed due to resource and time constraints. Years ago, this was a requirement that everyone struggled with, both vendor and customer.  Since that time there have been significant advances. Vendors see FIPS certification as a market advantage and Open-Source communities have stepped up to the challenge.  The benefit of effectively flipping a switch on a piece of software via money or time is limited at this stage of the project.  OpenSSL is used but without the FIPS.

## Implementation  

Away we go!!!!

First download your tools and get them installed
[Tools](https://mre-pi.com/Cybersecurity%20Tools/Tools.html) 

