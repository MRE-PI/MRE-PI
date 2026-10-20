---
nav_order: 4
layout: default
title: OS Hardening
parent: Implementation
nav_enabled: true
---

#### ** *V-238380* - The  operating system must disable the x86 Ctrl-Alt-Delete key sequence. **

Configure the system to disable the Ctrl-Alt-Delete sequence for the command line with the following commands:

```markdown
$ sudo systemctl mask ctrl-alt-del.target
```

Reload the daemon to take effect:  
```markdown
$ sudo systemctl daemon-reload  
```
#### *V-238200* - The Ubuntu operating system must allow users to directly initiate a session lock for all connection types.  
```markdown
sudo apt-get install vlock  
```

#### *V-270656* 24.04 LTS must have the "auditd" package installed. 
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
#### *V-238201* - The operating system must map the authenticated identity to the user or group account for PKI-based authentication. If the system is missing an "/etc/pam_pkcs11/" directory and an "/etc/pam_pkcs11/pam_pkcs11.conf", find an example to copy into place and modify accordingly at "/usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example.gz".  
```markdown
sudo cp /usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example /etc/pam_pkcs11/pam_pkcs11.conf  
```
#### *V-238330* - The operating system must disable account identifiers (individuals, groups, roles, and devices) after 35 days of inactivity.
```markdown
sudo useradd -D -f 35
```
#### *V-238333* - The operating system must be configured to use TCP syncookies.
```markdown
sudo nano /etc/sysctl.d/98-rpi.conf
```
add net.ipv4.tcp_syncookies = 1 then save file  

#### The following multiple V-IDs can be resolved with edits to /etc/login.defs  
#### *V-238209* - The operating system default filesystem permissions must be defined in such a way that all authenticated users can read and modify only their own files.  
#### *V-238325* - The operating system must encrypt all stored passwords with a FIPS 140-2 approved cryptographic hashing algorithm.  
#### *V-238202* - The operating system must enforce 24 hours/1 day as the minimum password lifetime. Passwords for new users must have a 24 hours/1 day minimum password lifetime restriction.  
#### *V-238203* - The operating system must enforce a 60-day maximum password lifetime restriction. Passwords for new users must have a 60-day maximum password lifetime restriction.

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

#### *V-274859* - 20.04 LTS must require users to provide a password for privilege escalation.  
check if file in /etc/sudoers.d that Include NOPASSWD
```markdown
##sudo rm /etc/sudoers.d/010_pi-nopasswd
```
#### *V-251504* - The operating system must not allow accounts configured with blank or null passwords.  
```markdown
sudo nano /etc/pam.d/common-auth
```
Remove or comment out the line:  
auth  [success=2 default=ignore]      pam_unix.so nullok  

#### The following multiple V-IDs can be resolved with edits to /etc/ssh/sshd_config  
#### *V-238218* - The operating system must not allow unattended or automatic login via SSH.  
#### *V-238219* - The operating system must be configured so that remote X connections are disabled, unless to fulfill documented and validated mission requirements.  
#### *V-238210* - The operating system must implement smart card logins for multifactor authentication for local and network access to privileged and nonprivileged accounts.  
#### *V-238211* - The operating system must use strong authenticators in establishing nonlocal maintenance and diagnostic sessions.  
#### *V-238212* - The operating system must immediately terminate all network connections associated with SSH traffic after a period of inactivity  
#### *V-238213* - The operating system must immediately terminate all network connections associated with SSH traffic at the end of the session or after 10 minutes of inactivity.  
#### *V-238214* - The operating system must display the Standard Mandatory DOD Notice and Consent Banner before granting any local or remote connection to the system.
#### *V-238216* - The operating system must configure the SSH daemon to use Message Authentication Codes (MACs) employing FIPS 140-2 approved cryptographic hashes to prevent the unauthorized disclosure of information and/or detect changes to information during transmission.  
#### *V-238217* - The operating system must configure the SSH daemon to use FIPS 140-2 approved ciphers to prevent the unauthorized disclosure of information and/or detect changes to information during transmission.  
#### *V-238220* - The operating system SSH daemon must prevent remote hosts from connecting to the proxy display.  

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
Ciphers aes256-ctr,aes192-ctr,aes128-ctr  
PubkeyAuthentication yes  
AuthorizedKeysFile      .ssh/authorized_keys .ssh/authorized_keys2   
```markdown
sudo systemctl restart sshd.service
```

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
#### *V-238371* - The operating system must use a file integrity tool to verify correct operation of all security functions.
#### *V-238303* - The operating system must use cryptographic mechanisms to protect the integrity of audit tools.  
```markdown
sudo aideinit  
```
```markdown
##sudo nano /etc/pam.d/login
```
session required pam_lastlog.so showfailed   

#### *V-238370* - The operating system must be configured so that Advance Package Tool (APT) removes all software components after updated versions have been installed.  
```markdown
##sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```
Unattended-Upgrade::Remove-Unused-Dependencies "true";  
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";  

#### *V-238323* - The operating system must limit the number of concurrent sessions to ten for all accounts and/or account types.
```markdown
##sudo nano /etc/security/limits.conf  
```
Edit record at bottom of file replacing "student" Note: "*" is part of record  
*   hard maxlogins 10  

###PWQUALITY
**Be very careful**
#### *V-238225* - The operating system must enforce a minimum 15-character password length.  
#### *V-238227* - The operating system must prevent the use of dictionary words for passwords.  
#### *V-238228* - The operating system must be configured so that when passwords are changed or new passwords are established, pwquality must be used.  
#### *V-238221* - The operating system must enforce password complexity by requiring that at least one upper-case character be used.  
#### *V-238222* - The operating system must enforce password complexity by requiring that at least one lower-case character be used.  
#### *V-238223* - The operating system must enforce password complexity by requiring that at least one numeric character be used.  
#### *V-238226* - The operating system must enforce password complexity by requiring that at least one special character be used.  
#### *V-238224* - The operating system must require the change of at least 8 characters when passwords are changed.  
  
```markdown
sudo nano /etc/security/pwquality.conf  
```
Make the following edits  
minlen=15  
dictcheck=1
enforcing = 1  
ucredit=-1
lcredit=-1
dcredit=-1
ocredit=-1  
- difok=8  be cautiuos with this one

#### *V-238228* - The Ubuntu operating system must be configured so that when passwords are changed or new passwords are established, pwquality must be used.  

```markdown
sudo apt-get install libpam-pwquality -y
```
Add the following line to "/etc/security/pwquality.conf" (or modify the line to have the required value):
```markdown
sudo nano /etc/security/pwquality.conf  
```
enforcing = 1  

Add the following line to "/etc/pam.d/common-password" (or modify the line to have the required value):  
```markdown
sudo nano /etc/pam.d/common-password  
```
password requisite pam_pwquality.so retry=3  

#### *V-238338* - The operating system must configure the /var/log directory to be group-owned by syslog   
Pi Os - Debian 13 (Trixie) does not use syslog.  It uses **journlctl** instead
```markdown 
~~sudo chgrp syslog /var/log~~
```
#### *V-238341* - The operating system must configure the /var/log/syslog file to be group-owned by adm.  
Pi Os - Debian 13 (Trixie) does not use syslog.  It uses **journlctl** instead
```markdown
~~sudo chgrp adm /var/log/syslog~~
```
#### *V-238343* - The operating system must configure /var/log/syslog file with mode 0640 or less permissive.  
Pi Os - Debian 13 (Trixie) does not use syslog.  It uses **journlctl** instead
```markdown
~~sudo chmod 0640 /var/log/syslog~~  
```
#### *V-238348*
- The operating system library directories must have mode 0755 or less permissive.  
```markdown 
sudo find /lib /lib64 /usr/lib -perm /022 -type d -exec chmod 755 '{}' \;  
```
#### *V-238351*  
- The operating system library files must be group-owned by root or a system account.
```markdown
$ sudo find /lib /lib64 /usr/lib /usr/lib64 -type f -name '*.so*' ! -group root -exec chown :root {} +  
```
#### *V-251505* - The Ubuntu operating system must disable automatic mounting of Universal Serial Bus (USB) mass storage driver.  
```markdown 
sudo su -c "echo install usb-storage /bin/false >> /etc/modprobe.d/DISASTIG.conf"  
```
```markdown
sudo su -c "echo blacklist usb-storage >> /etc/modprobe.d/DISASTIG.conf"
```
#### *V-255912* - The Ubuntu operating system SSH server must be configured to use only FIPS-validated key exchange algorithms.  
```markdown
sudo nano /etc/ssh/sshd_config
```
Add "#Configure the SSH server to use only FIPS-validated key exchange algorithms" as a comment.
Add KexAlgorithms ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256  
Then restart sshd  
```markdown
sudo systemctl restart sshd
```
#### *V-238360* - The Ubuntu operating system must be configured to use AppArmor.  
```markdown
sudo apt-get install apparmor
```
```markdown
sudo systemctl enable apparmor.service 
```
```markdown
sudo systemctl start apparmor.service 
```
#### *V-238354* - The Ubuntu operating system must have an application firewall installed in order to control remote access methods.  

```markdown
sudo apt-get install ufw
```
#### *V-238367* - The Ubuntu operating system must configure the uncomplicated firewall to rate-limit impacted network interfaces.  
```markdown
sudo ufw limit http
```
```markdown
sudo ufw limit ssh  
```
  
~~~ #### *V-238353* ~~~
~~~ - The operating system must be configured to preserve log records from failure events.  ~~~

~~~Install the log service (if the log service is not already installed) with the following command: ~~~
Raspberry Pi OS (Trixe) uses **journalctl** not syslog  
```markdown 
~~~$ sudo apt-get install rsyslog ~~~
```
~~~ Enable the log service with the following command: ~~~

```markdown 
~~~ $ sudo systemctl enable --now rsyslog ~~~
```
```markdown 
++##sudo nano /etc/chrony/chrony.conf
```

makestep 1 -1  
```markdown
##sudo find /var/log -perm /137 ! -name '*[bw]tmp' ! -name '*lastlog' -type f -exec chmod 640 '{}' \;  
```
