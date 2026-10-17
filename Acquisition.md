---
nav_order: 7
layout: default
title: Acquisition
nav_enabled: true
---

# Asset Procurement & Acquisition

US Federal Acquisition rules can be quite complex but there are a few rules that are important  

TAA Compliance  
: Required under FAR 52.225‑5 for federal procurement. Products must be either:  
U.S.‑made end products, or  
Designated‑country end products, or  
Foreign end products that have undergone substantial transformation in a designated country.  

From a cybersecurity perspective this is especially important with respect to cryptographic infrastructure  
Practically it can become an exercise in semantics but in practice it ensures products are evaluated based on more than cost and functionality.  There are numerous examples of products that camouflage their country of origin. Alternately, there are examples of compliant small companies that can't compete on price and volume but may require a little extra detective work to find.  

Unfortunately, due to world events procurment is the most difficult part of replicating this project.  The AI explosion and realworld Warfare has made all circuitboards and memory difficult to obtain. Oldtimers such as myself and some academic environments may have equipment on hand, otherwise tools such as [RPILocator](https://rpilocator.com) are your best bet.  
I will provide sources that used to be the best to allow you to capture product metadata more easily  

Raspberry Pi 5  
I used the CM5 to minimize size for the Outdoor hardened enclosure.  A regular Raspberry Pi 4 or 5 will work.  A Pi 3 is ok but may not have the processing power to meet the project requirements.  
As the CM5 is barebones, I had to add the following:  

[Waveshare CM4/CM5 Adapter Board, Comaptible with Raspberry Pi Compute Module Series, Interface Protection](https://www.amazon.com/dp/B0F9FMQFMD?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_6)  
[GeeekPi N10 Tiny PCIe M.2 Key-M NVMe SSD PCIe Peripheral Board for Raspberry Pi 5](https://www.amazon.com/dp/B0D2LCKV5N?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_6)  

Raspberry Pi 2W  
I prefer without the header, but different use cases could require it.   
[Raspberry Pi Zero 2 W](https://www.adafruit.com/product/5291)  

SD Cards  
Name Brand SD cards like SanDisk are mandatory.  Off brands will cause issues and waste your time.  

NestOut Batteries  
I highly recommend these batteries for outdoor use.  I have field tested them with great success a raspberry pi will last 36hrs unmodified on the 15K NestOut
GigaPower Batteries  
For the Gateway the wireless transmissions burn up double the power of the othe devices.  The GigaPower 30k will meet the requirement but there are other options as well (NestOut Powerstaion, Jackery Ultra)

Recommended Cables and Cases.  

YubiKey
