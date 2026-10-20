---
nav_order: 5
layout: default
title: NGINX Hardening
parent: OS Hardening
nav_enabled: true
---

#### *V-278394* - NGINX must restrict the ability of individuals to launch denial-of-service (DoS) attacks against other information systems.  

```markdown  
sudo nano /etc/nginx/nginx.conf  
```
Under http add the following:  

client_body_timeout 10s;  
client_header_timeout 10s;  
send_timeout 10s;  

#### *V-278399* - NGINX must be configured to require SSL sessions to reauthenticate no longer than 15 minutes.  

```markdown  
sudo nano /etc/nginx/nginx.conf  
```
Under  # SSL Settings add  
ssl_session_timeout 15m;  

#### *V-278405* - NGINX must be configured to use FIPS-approved algorithms to protect the confidentiality and integrity of transmitted information.  

```markdown  
sudo nano /etc/nginx/nginx.conf  
```
Under  # SSL Settings add  
ssl_ciphers 'TLS_AES_256_GCM_SHA384:TLS_AES_128_GCM_SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-GCM-SHA256:ECD>
ssl_prefer_server_ciphers on # Force server cipher order.

#### *V-278408* - The NGINX service account must be configured to lock changes to the password.  

Identify the NGINX runtime user:  
```markdown
grep -E '^\s*user\s+' /etc/nginx/nginx.conf  
```
Confirm the password is locked:
```markdown
passwd -S nginx
```
Lock the password for the NGINX user (if not already locked):
```markdown
sudo passwd -l nginx
```
