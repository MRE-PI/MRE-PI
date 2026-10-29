---
nav_order: 6
layout: default
title: OS Hardening
parent: Implementation
nav_enabled: true
---

#### ** *V-238380* - The  operating system must disable the x86 Ctrl-Alt-Delete key sequence. **

Configure the system to disable the Ctrl-Alt-Delete sequence for the command line with the following commands:

```markdown
sudo systemctl mask ctrl-alt-del.target
```

Reload the daemon to take effect:  
```markdown
sudo systemctl daemon-reload  
```
#### *V-238200* - The Ubuntu operating system must allow users to directly initiate a session lock for all connection types.  
#### *V-270656* 24.04 LTS must have the "auditd" package installed. 
#### *V-270653* - Ubuntu 24.04 LTS must be configured to preserve log records from failure events.  
```markdown
sudo apt install vlock auditd rsyslog -y
```
```markdown
sudo apt install sssd opensc libpam-pkcs11 ufw libpam-pwquality apparmor pcscd pcsc-tools aide chrony -y
```
```markdown
sudo auditd -s enable
```
With auditd enabled the following are additional configuration actions  

```markdown
sudo systemctl enable auditd.service
```
```markdown
sudo systemctl enable --now rsyslog
```
```markdown
sudo nano /etc/audit/rules.d/stig.rules
```
create/copy/paste audit rules.txt  

```markdown
sudo chmod -R 0640 /etc/audit/rules.d
```
#### *V-270657* - Ubuntu 24.04 LTS must produce audit records and reports containing information to establish when, where, what type, the source, and the outcome for all DOD-defined auditable events and actions in near real time. 
```markdown
sudo systemctl enable auditd.service  
```
**To reload the rules file, issue the following command:**  
```markdown
sudo augenrules --load
```
#### *V-270765* - Ubuntu 24.04 LTS must configure the /var/log directory to be group-owned by syslog.  
#### *V-270768* - Ubuntu 24.04 LTS must configure the /var/log/syslog file to be group-owned by adm.  
#### *V-270769* - Ubuntu 24.04 LTS must configure /var/log/syslog file to be owned by syslog.  
#### *V-270770* - Ubuntu 24.04 LTS must configure /var/log/syslog file with mode "0640" or less permissive.  

```markdown
sudo chgrp syslog /var/log  
```
```markdown
sudo chgrp adm /var/log/syslog  
```
```markdown
sudo chown syslog /var/log/syslog  
```
```markdown
sudo chmod 0640 /var/log/syslog  
```

#### *V-270757* - Ubuntu 24.04 LTS must generate system journal entries without revealing information that could be exploited by adversaries.  
Create the following new file:  
```markdown
sudo nano /etc/tmpfiles.d/zzz-systemd-stig.conf
```
Edit and add
```markdown
z /run/log/journal 0640 root systemd-journal - -
Z /run/log/journal/%m ~0640 root systemd-journal - -
z /var/log/journal 0640 root systemd-journal - -
z /var/log/journal/%m 0640 root systemd-journal - -
z /var/log/journal/%m/system.journal 0640 root systemd-journal - -
```

#### *V-238201* - The operating system must map the authenticated identity to the user or group account for PKI-based authentication. If the system is missing an "/etc/pam_pkcs11/" directory and an "/etc/pam_pkcs11/pam_pkcs11.conf", find an example to copy into place and modify accordingly at "/usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example.gz".  
```markdown
sudo cp /usr/share/doc/libpam-pkcs11/examples/pam_pkcs11.conf.example /etc/pam_pkcs11/pam_pkcs11.conf
```
#### *V-270663* - Ubuntu 24.04 LTS must use the "SSSD" package for multifactor authentication services.  
```markdown
sudo systemctl enable sssd.service 
```
```markdown
sudo systemctl start sssd.service 
```

#### *V-238330* - The operating system must disable account identifiers (individuals, groups, roles, and devices) after 35 days of inactivity.
```markdown
sudo useradd -D -f 35
```
#### *V-238333* - The operating system must be configured to use TCP syncookies.
```markdown
sudo nano /etc/sysctl.d/98-rpi.conf
```
add 
``markdown
net.ipv4.tcp_syncookies = 1
```
then save file  

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
#### *V-238228* - The Ubuntu operating system must be configured so that when passwords are changed or new passwords are established, pwquality must be used.  

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
enforcing = 1  
- difok=8  be cautiuos with this one



```markdown
sudo apt-get install libpam-pwquality -y
```
Add the following line to "/etc/security/pwquality.conf" (or modify the line to have the required value):
```markdown
sudo nano /etc/security/pwquality.conf  
```
  

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
sudo find /lib /lib64 /usr/lib /usr/lib64 -type f -name '*.so*' ! -group root -exec chown :root {} +  
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
  
#### *V-238353*
~~- The operating system must be configured to preserve log records from failure events.~~

~~Install the log service (if the log service is not already installed) with the following command:~~  
Raspberry Pi OS (Trixe) uses **journalctl** not syslog  
~~```markdown~~
--sudo apt-get install rsyslog--
~~```~~
~~Enable the log service with the following command:~~

#### *V-270725* - Ubuntu 24.04 LTS must store only encrypted representations of passwords.  
```markdown
sudo nano /etc/pam.d/common-password
```
Edit or change to as follows:
password [success=1 default=ignore] pam_unix.so obscure sha512 shadow rounds=100000  

#### *V-270724* - Ubuntu 24.04 LTS must prevent direct login to the root account.  
Missleading result from sudo passwd -S root returns
root L 2025-12-04 0 99999 7 -1
Instead of the Ubuntu Result
root L 04/08/2024 0 99999 7 -1 

#### *V-270758* - Ubuntu 24.04 LTS must be configured so that the "journalctl" command is not accessible by unauthorized users.  
```markdown
sudo chmod 740 /usr/bin/journalctl
```
#### *V-270827* - Ubuntu 24.04 LTS must be configured so that audit log files are not read or write-accessible by unauthorized users.  
```markdown
sudo chmod 0600 /var/log/audit/*
```
#### *V-270829* - Ubuntu 24.04 LTS must permit only authorized groups ownership of the audit log files.  
```markdown
sudo sed -i '/^log_group/D' /etc/audit/auditd.conf
```
```markdown
sudo sed -i /^log_file/a'log_group = root' /etc/audit/auditd.conf
```
#### *V-270649* - Ubuntu 24.04 LTS must use a file integrity tool to verify correct operation of all security functions.  
```markdown
sudo apt install -y aide
```
#### *V-270652* - Ubuntu 24.04 LTS must notify designated personnel if baseline configurations are changed in an unauthorized manner. The file integrity tool must notify the system administrator (SA) when changes to the baseline configuration or anomalies in the operation of any security functions are discovered. 
```markdown
sudo nano /etc/default/aide
```
#### *V-270831* - Ubuntu 24.04 LTS must use cryptographic mechanisms to protect the integrity of audit tools.  
```markdown
sudo nano /etc/aide/aide.conf  
```
append to file  
```markdown
# Audit Tools 
/sbin/auditctl p+i+n+u+g+s+b+acl+xattrs+sha512  
/sbin/auditd p+i+n+u+g+s+b+acl+xattrs+sha512  
/sbin/ausearch p+i+n+u+g+s+b+acl+xattrs+sha512  
/sbin/aureport p+i+n+u+g+s+b+acl+xattrs+sha512  
/sbin/autrace p+i+n+u+g+s+b+acl+xattrs+sha512  
/sbin/augenrules p+i+n+u+g+s+b+acl+xattrs+sha512  
```


remove the comment mark # from "SILENTREPORTS=no"

#### *V-270680* - Ubuntu 24.04 LTS must automatically terminate a user session after inactivity timeouts have expired.  
```markdown
sudo nano /etc/profile.d/99-terminal_tmout.sh
```
add to file
```markdown
TMOUT=600
```
#### *V-270681* - Ubuntu 24.04 LTS must monitor remote access methods.  

```markdown
sudo nano  /etc/rsyslog.d/50-default.conf
```
Add
```markdown
auth.*,authpriv.* /var/log/secure 
daemon.* /var/log/messages 
```
sudo systemctl restart rsyslog.service  if needed

#### *V-270691* - Ubuntu 24.04 LTS must display the Standard Mandatory DOD Notice and Consent Banner before granting access to via an SSH logon.
This is purely a placeholder.  It is modified to identify the system as a training system
```markdown
sudo nano /etc/issue.net
```
Add banner statement to the file.

```markdown
"This is a Cybersecurity Training System and not owned or monitored by the USG.  Notwithstanding the following does apply.  The entity USG is replaced by the entity performing the training.
"You are accessing a U.S. Government (USG) Information System (IS) that is provided for USG-authorized use only. 

By using this IS (which includes any device attached to this IS), you consent to the following conditions: 

-The USG routinely intercepts and monitors communications on this IS for purposes including, but not limited to, penetration testing, COMSEC monitoring, network operations and defense, personnel misconduct (PM), law enforcement (LE), and counterintelligence (CI) investigations. 

-At any time, the USG may inspect and seize data stored on this IS. 

-Communications using, or data stored on, this IS are not private, are subject to routine monitoring, interception, and search, and may be disclosed or used for any USG-authorized purpose. 

-This IS includes security measures (e.g., authentication and access controls) to protect USG interests--not for your personal benefit or privacy. 

-Notwithstanding the above, using this IS does not constitute consent to PM, LE or CI investigative searching or monitoring of the content of privileged communications, or work product, related to personal representation or services by attorneys, psychotherapists, or clergy, and their assistants. Such communications and work product are private and confidential. See User Agreement for details." 

```
sudo nano /etc/ssh/sshd_config  
Modify  
"#Banner none" to "Banner /etc/issue.net"  

#### *V-270754* - Ubuntu 24.04 LTS must configure the uncomplicated firewall to rate-limit impacted network interfaces.  

```markdown
sudo ufw enable  
```
List current ufw rules  
```markdown
sudo ufw status verbose
```
For this project add port 8080
```markdown
sudo ufw limit 8080  
```
#### *V-274868* - Ubuntu 24.04 LTS must require users to provide a password for privilege escalation.  
```markdown
sudo find /etc/sudoers /etc/sudoers.d -type f -exec sed -i '/NOPASSWD/ s/^/# /g' {} \;  
```


```markdown
sudo systemctl enable --now rsyslog
```
```markdown 
sudo nano /etc/chrony/chrony.conf
```

#### *V-238337* - The Ubuntu operating system must generate error messages that provide information necessary for corrective actions without revealing information that could be exploited by adversaries.
```markdown 
sudo find /var/log -perm /137 ! -name '*[bw]tmp' ! -name '*lastlog' -type f -exec chmod 640 '{}' \;  
```
#### *V-238348* - The Ubuntu operating system library directories must have mode 0755 or less permissive.
fox-admin@PiMotion412:/usr/sbin $ sudo find /lib /lib64 /usr/lib -perm /022 -type d -exec chmod 755 '{}' \;
**find: ‘/lib64’: No such file or directory**


makestep 1 -1  
```markdown
##sudo find /var/log -perm /137 ! -name '*[bw]tmp' ! -name '*lastlog' -type f -exec chmod 640 '{}' \;  
```
