---
nav_order: 4
layout: default
title: OS STIG
parent: Implementation
nav_enabled: true
---

#Scanning the Operating System against the STIG Checklist

It is assumed you successfully navigated the installation of the latest version of SCC.  
A key understanding upfront is that via these instructions you are to:
- Scan via a Windows Laptop that is within the network boundary of your test targets.
- Utilize the Ubuntu STIG that maps to the version of Debian/Raspberry Pi OS that you are using (Ubuntu 24 arm64 = Trixie on Raspberry Pi 3, 4, & 5)
  There are Raspberry Pi selections available in SCC but are for legacy versions (i.e. Bookworm, Bullseye or Jessie)
- Use the results to manually harden an asset.  Later we will explore automation methods such as USG (Ubuntu Security Guide)

- 
