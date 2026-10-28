---
nav_order: 4
layout: default
title: FIPS 140-3
parent: Home
nav_enabled: true
---

Additional info WRT to FIPS 140-3
=================================

OpenSSL FIPS can be compiled from source on Raspberry Pi Systems, however an  
**Important distinction:**  

OpenSSL 3 FIPS support is provider-based:  
enable-fips  
fips.so / fips.dll  
openssl fipsinstall  
fipsmodule.cnf  

Distro/kernel FIPS mode is system-level:  
boot-time policy  
kernel/userland enforcement  
distro packages and validation hooks  
So:  
V-270744 - Ubuntu 24.04 LTS must implement NIST FIPS-validated cryptography  
**check text** /proc/sys/crypto/fips_enabled is an example of a distro/kernel-level FIPS indicator  
*but it is not what this OpenSSL/Pi OS Trixie repo is using.*  

The *OpenSSL/Pi OS Trixie repo* is using a provider model, not a Linux sysctl check  
If using Ubuntu 24.04 for this project the FIPs module is only availabel in the Pro version ($) and [not compatible with Raspberry Pi](https://github.com/canonical/ubuntu-pro-client/issues/3336)  
The Ubuntu Server package for Raspberry Pi is an additional 2/3 larger than the Pi OS Lite Package.  

The Debian unstable branch has OpenSSL Kernel mode which could be applied to Pi OS but I am uncertain of its success.   

So, to reiterate, for this current phase of the project FIPS is not worth the $ or time for a training exersize.  

