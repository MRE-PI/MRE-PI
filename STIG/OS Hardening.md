---
nav_order: 4
layout: default
title: OS Hardening
parent: Implementation
nav_enabled: true
---

#### *V-238380* - The Ubuntu operating system must disable the x86 Ctrl-Alt-Delete key sequence.

Configure the system to disable the Ctrl-Alt-Delete sequence for the command line with the following commands:

```markdown
$ sudo systemctl mask ctrl-alt-del.target
```

Reload the daemon to take effect:  
```markdown
$ sudo systemctl daemon-reload  
```

#### *V-270656* Ubuntu 24.04 LTS must have the "auditd" package installed. 
```markdown
sudo apt install auditd
```
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
#### *V-238201* - The Ubuntu operating system must map the authenticated identity to the user or group account for PKI-based authentication. If the system is missing an "/etc/pam_pkcs11/" directory and an "/etc/pam_pkcs11/pam_pkcs11.conf", find an example to copy into place and modify accordingly at "/usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example.gz".  
```markdown
sudo cp /usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example /etc/pam_pkcs11/pam_pkcs11.conf  
```
#### *V-238330* - The Ubuntu operating system must disable account identifiers (individuals, groups, roles, and devices) after 35 days of inactivity.
```markdown
sudo useradd -D -f 35
```
#### *V-238333* - The Ubuntu operating system must be configured to use TCP syncookies.
```markdown
sudo nano /etc/sysctl.d/98-rpi.conf
```
add net.ipv4.tcp_syncookies = 1 then save file  

#### The following multiple V-IDs can be resolved with edits to /etc/login.defs  
#### *V-238209* - The Ubuntu operating system default filesystem permissions must be defined in such a way that all authenticated users can read and modify only their own files.  
#### *V-238325* - The Ubuntu operating system must encrypt all stored passwords with a FIPS 140-2 approved cryptographic hashing algorithm.  
#### *V-238202* - The Ubuntu operating system must enforce 24 hours/1 day as the minimum password lifetime. Passwords for new users must have a 24 hours/1 day minimum password lifetime restriction.  
#### *V-238203* - The Ubuntu operating system must enforce a 60-day maximum password lifetime restriction. Passwords for new users must have a 60-day maximum password lifetime restriction.

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

#### *V-274859* - Ubuntu 20.04 LTS must require users to provide a password for privilege escalation.  
check if file in /etc/sudoers.d that Include NOPASSWD
```markdown
##sudo rm /etc/sudoers.d/010_pi-nopasswd
```
#### *V-251504* - The Ubuntu operating system must not allow accounts configured with blank or null passwords.  
```markdown
sudo nano /etc/pam.d/common-auth
~~~
Remove or comment out the line:  
auth  [success=2 default=ignore]      pam_unix.so nullok  

#### The following multiple V-IDs can be resolved with edits to /etc/ssh/sshd_config  
#### *V-238218* - The Ubuntu operating system must not allow unattended or automatic login via SSH.  
#### *V-238219* - The Ubuntu operating system must be configured so that remote X connections are disabled, unless to fulfill documented and validated mission requirements.  
#### *V-238210* - The Ubuntu operating system must implement smart card logins for multifactor authentication for local and network access to privileged and nonprivileged accounts.  
#### *V-238211* - The Ubuntu operating system must use strong authenticators in establishing nonlocal maintenance and diagnostic sessions.  
#### *V-238212* - The Ubuntu operating system must immediately terminate all network connections associated with SSH traffic after a period of inactivity  
#### *V-238213* - The Ubuntu operating system must immediately terminate all network connections associated with SSH traffic at the end of the session or after 10 minutes of inactivity.  
#### *V-238214* - The Ubuntu operating system must display the Standard Mandatory DOD Notice and Consent Banner before granting any local or remote connection to the system.
#### *V-238216* - The Ubuntu operating system must configure the SSH daemon to use Message Authentication Codes (MACs) employing FIPS 140-2 approved cryptographic hashes to prevent the unauthorized disclosure of information and/or detect changes to information during transmission.  
#### *V-238217* - The Ubuntu operating system must configure the SSH daemon to use FIPS 140-2 approved ciphers to prevent the unauthorized disclosure of information and/or detect changes to information during transmission.  
#### *V-238220* - The Ubuntu operating system SSH daemon must prevent remote hosts from connecting to the proxy display.  

```markdown
sudo nano /etc/ssh/sshd_config
```
Make the following edits  
PermitEmptyPasswords no  
PermitUserEnvironment no  
ClientAliveCountMax 1  
ClientAliveInterval 600  
X11UseLocalhost yes  
X11Forwarding no  
MACs hmac-sha2-512,hmac-sha2-256 
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
#### *V-238371* - The Ubuntu operating system must use a file integrity tool to verify correct operation of all security functions.
#### *V-238303* - The Ubuntu operating system must use cryptographic mechanisms to protect the integrity of audit tools.  
```markdown
sudo aideinit  
```
```markdown
##sudo nano /etc/pam.d/login
```
session required pam_lastlog.so showfailed   

#### *V-238370* - The Ubuntu operating system must be configured so that Advance Package Tool (APT) removes all software components after updated versions have been installed.  
```markdown
##sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```
Unattended-Upgrade::Remove-Unused-Dependencies "true";  
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";  

#### *V-238323* - The Ubuntu operating system must limit the number of concurrent sessions to ten for all accounts and/or account types.
```markdown
##sudo nano /etc/security/limits.conf  
```
Edit record at bottom of file replacing "student" Note: "*" is part of record  
*   hard maxlogins 10  
```markdown 
++##sudo nano /etc/chrony/chrony.conf
```

makestep 1 -1  
```markdown
##sudo find /var/log -perm /137 ! -name '*[bw]tmp' ! -name '*lastlog' -type f -exec chmod 640 '{}' \;  
```
