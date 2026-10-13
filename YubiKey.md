---
nav_order: 13
layout: default
title: Yubikey & Putty Setup
parent: Implementation
nav_enabled: true
---

## Yubikey  
Copying down your PIV Public Key from your Yubikey is one of the first steps to the project  
Instructions are clearly documented on the [Yubikey website](https://developers.yubico.com/PIV/)  
The bottom line upfront (BLUF) is you need the Yubikey device to generate the key in slot 9A and export the public key in the correct SSH format and add it to authorized_keys on the target system.  
The tool to do this is YubiKey Manager, also referred to as ykman.  It is a general-purpose tool for the configuration of all of the functions of the YubiKey.
There is an additional tool "yubico-piv-tool" more targeted for use on linux.  It is up to the individual to select which YubiKey tool. ykman is my recommendation as the physical key is installed on the remote laptop for authentication to the remote raspberry assets.

## Putty-CAC

[https://pivkey.zendesk.com/hc/en-us/articles/207698876-PIVKey-and-PuTTY-CAC-for-SSH-on-Windows]
