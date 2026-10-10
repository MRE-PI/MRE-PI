---
nav_order: 1
layout: default
title: Home
nav_enabled: true
---

# Securing a Raspberry Pi to Military Standards #

Project Requirements:  
    [1. Follow a simplified Acquisition and Systems Engineering Process](https://www.linkedin.com/pulse/cybersecurity-process-integration-v-model-development-jadhav-dvnpc/)  
    3. Focus on Cybersecurity and not the Platform.  The platform is tailored for specific Cybersecurity use cases.  
    4. The platform is to be a real-world platform not a rock sitting in a safe.  
    
## Instantiated requirements ##

### Hardware: ###

Video  Camera
:  Video is easily implemented on the entire suite of Raspberry Pi products.  It is in effect a sensor.  It could be substituted with a microphone, a temperature sensor, etc.  

Edge architecture  
: Communications are always a key architecture requirement for Military, whether mobility, encryption requirements.  
It should be assumed for this exercise only publicly available communications & encryption will be used. However, there are plenty of examples that can be utilized without the acquisition of a TAClane or LinkX communications.  

WIFI Router (1)  
Edge Server (1)  
Sensors (3)  
[Figure 1](https://robert-brown19.github.io/apple-pi/Figure1.html)  

### Software: ###

Motion v5 
: Motion is a program that monitors the signal from video cameras and detects changes in the images.

NGINX 
: Motion supported Webserver configuration option which after Apache Tomcat is very common

MariaDB 
: A database supported by Motion selected because it is covered by a published Security Technical Implementation Guide (STIG)
