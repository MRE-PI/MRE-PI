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
V-270744 - Ubuntu 24.04 LTS must implement NIST FIPS-validated cryptography **check text**    
/proc/sys/crypto/fips_enabled is an example of a distro/kernel-level FIPS indicator  
but it is not what this OpenSSL repo is using  
this repo is using the OpenSSL provider model, not a Linux sysctl check  
