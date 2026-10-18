---
nav_order: 4
layout: default
title: OS Hardening
parent: Implementation
nav_enabled: true
---
### *V-270656* Ubuntu 24.04 LTS must have the "auditd" package installed.  
```markdown
sudo auditd -s enable
```
With auditd enabled the following are additional configuration actions  

```markdown
sudo systemctl enable auditd.service
```
```markdown
sudo nano /etc/audit/rules.d/stig.rules
```
create/copy/paste audit rules.txt  
```markdown
sudo augenrules --load
```
```markdown
sudo chmod -R 0640 /etc/audit/rules.d
```
### *V-238201* - The Ubuntu operating system must map the authenticated identity to the user or group account for PKI-based authentication. If the system is missing an "/etc/pam_pkcs11/" directory and an "/etc/pam_pkcs11/pam_pkcs11.conf", find an example to copy into place and modify accordingly at "/usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example.gz".  
```markdown
sudo cp /usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example /etc/pam_pkcs11/pam_pkcs11.conf  
```
### *V-238330* - The Ubuntu operating system must disable account identifiers (individuals, groups, roles, and devices) after 35 days of inactivity.
```markdown
sudo useradd -D -f 35
```
### *V-238333* - The Ubuntu operating system must be configured to use TCP syncookies.
```markdown
sudo nano /etc/sysctl.conf
```
uncomment net.ipv4.tcp_syncookies = 1 then save file  

### The following multiple V-IDs can be resolved with edits to /etc/login.defs  
### *V-238209* - The Ubuntu operating system default filesystem permissions must be defined in such a way that all authenticated users can read and modify only their own files.  
### *V-238325* - The Ubuntu operating system must encrypt all stored passwords with a FIPS 140-2 approved cryptographic hashing algorithm.  
### *V-238202* - The Ubuntu operating system must enforce 24 hours/1 day as the minimum password lifetime. Passwords for new users must have a 24 hours/1 day minimum password lifetime restriction.  
### *V-238203* - The Ubuntu operating system must enforce a 60-day maximum password lifetime restriction. Passwords for new users must have a 60-day maximum password lifetime restriction.

```markdown
sudo nano /etc/login.defs  
```
Make the following edits  
UMASK 077  
ENCRYPT_METHOD SHA512  
PASS_MIN_DAYS 1  
PASS_MAX_DAYS 60  

```markdown
sudo nano /etc/pam.d/login
```
Make the following edits  
session required pam_lastlog.so showfailed  
+++++Remove any occurrence of "NOPASSWD" or "!authenticate" found in "/etc/sudoers" file or files in the "/etc/sudoers.d" directory.  
```markdown
##sudo rm /etc/sudoers.d/010_pi-nopasswd
```
```markdown
##sudo nano /etc/ssh/sshd_config
```
Make the following edits  
PermitEmptyPasswords no  
PermitUserEnvironment no  
ClientAliveCountMax 1  
ClientAliveInterval 600  
X11UseLocalhost yes  
X11Forwarding no  
PubkeyAuthentication yes  
AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2   
```markdown
mkdir ~/.ssh
```
```markdown
sudo nano ~/.ssh/authorized_keys
```
copy key into file  
```markdown
sudo systemctl restart sshd.service
```
```markdown
sudo aideinit  
```
```markdown
##sudo nano /etc/pam.d/login
```
session required pam_lastlog.so showfailed   
```markdown
##sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```
Unattended-Upgrade::Remove-Unused-Dependencies "true";  
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";  
```markdown
##sudo nano /etc/security/limits.conf
```
hard maxlogins 10  
```markdown 
++##sudo nano /etc/chrony/chrony.conf
```

makestep 1 -1  
```markdown
##sudo find /var/log -perm /137 ! -name '*[bw]tmp' ! -name '*lastlog' -type f -exec chmod 640 '{}' \;  
```
