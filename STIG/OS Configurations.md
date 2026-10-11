---
nav_order: 4
layout: default
title: OS Cfg
nav_enabled: true
---
```markdown
sudo auditd -s enable
```
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
```markdown
sudo cp /usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example /etc/pam_pkcs11/pam_pkcs11.conf  
```
```markdown
sudo useradd -D -f 35
```
```markdown
sudo nano /etc/sysctl.conf
```
uncomment net.ipv4.tcp_syncookies = 1 then save file  
```markdown
sudo nano /etc/login.defs  
```
Make the following edits  
UMASK 077  
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
