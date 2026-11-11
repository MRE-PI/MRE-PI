
Results: High Severity (CAT I)  
================================

### V-270675 - Ubuntu 24.04 LTS when booted must require authentication upon booting into single-user and maintenance mo des. - Fail
Not a typical feature on Raspberry Pi as it boots from an easily removeable SD Card.  Furth methods will be researched.  Physical protections would function as a mitigation. Locks, Tamper Detection, etc.
### V-270714 - Ubuntu 24.04 LTS must not allow accounts configured in Pluggable Authentication Modules (PAM) with blank or null passwords. - Fail
Fixed?
### V-270736 - Ubuntu 24.04 LTS must map the authenticated identity to the user or group account for PKI-based authentication. - Fail
Requires LDAP and full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270744 - Ubuntu 24.04 LTS must implement NIST FIPS-validated cryptography to protect classified information and for the following: To provision digital signatures, to generate cryptographic hashes, and to protect unclassified information requiring confidentiality and cryptographic protection in accordance with applicable federal laws, Executive Orders, directives, policies, regulations, and standards. - Fail
FIPS discussed in detail. Requires full enterprise PKI implementation with CA and revocation checking. Out of scope  

Results: Medium Severity (CAT II)  
=================================
 
### V-270663 - Ubuntu 24.04 LTS must use the "SSSD" package for multifactor authentication services. - Fail
Requires full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270676 - Ubuntu 24.04 LTS must initiate session audits at system startup. - Fail
PI OS does not utilize Grub
### V-270681 - Ubuntu 24.04 LTS must monitor remote access methods. - Fail
An error in the SCC code or unknow issue with PI OS implementation
### V-270691 - Ubuntu 24.04 LTS must display the Standard Mandatory DOD Notice and Consent Banner before granting access to via an SSH logon. - Fail
### V-270694 - Ubuntu 24.04 LTS must be configured to enforce the acknowledgement of the Standard Mandatory DOD Notice and Consent Banner for all SSH connections. - Fail
Out of scope. System is platform IT with no users.  Might as well put a fence around a satellite.
### V-270699 - Ubuntu 24.04 LTS library files must be group-owned by root or a system account. - Fail
An error in the SCC code or unknow issue with PI OS implementation
### V-270723 - Ubuntu 24.04 LTS must electronically verify Personal Identity Verification (PIV) credentials. - Fail
Requires full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270725 - Ubuntu 24.04 LTS must store only encrypted representations of passwords. - Fail
An error in the SCC code or unknow issue with PI OS implementation
### V-270737 - Ubuntu 24.04 LTS, for PKI-based authentication, Privileged Access Management (PAM) must validate certificates by constructing a certification path (which includes status information) to an accepted trust anchor. - Fail
Requires full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270738 - Ubuntu 24.04 LTS for PKI-based authentication, must implement a local cache of revocation data in case of the inability to access revocation information via the network. - Fail
Requires full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270756 - Ubuntu 24.04 LTS must generate error messages that provide information necessary for corrective actions without revealing information that could be exploited by adversaries. - Fail
An error in the SCC code or unknow issue with PI OS implementation
### V-270762 - Ubuntu 24.04 LTS must configure the files used by the system journal to be group-owned by "systemd-journal". - Fail
An error in the SCC code or unknow issue with PI OS implementation
### V-270769 - Ubuntu 24.04 LTS must configure /var/log/syslog file to be owned by syslog. - Unknown
An error in the SCC code or unknow issue with PI OS implementation
### V-270771 - Ubuntu 24.04 LTS must implement nonexecutable data to protect its memory from unauthorized code execution. - Fail
Raspberry PI does not have this feature in Pi Zero 2W but maybe Pi 4, 5
### V-270784 - Ubuntu 24.04 LTS must generate audit records for any use of the setxattr, fsetxattr, lsetxattr, removexattr, fremovexattr, and lremovexattr system calls. - Fail
### V-270785 - Ubuntu 24.04 LTS must generate audit records for successful/unsuccessful uses of the chown, fchown, fchownat, and lchown system calls. - Fail
### V-270786 - Ubuntu 24.04 LTS must generate audit records for successful/unsuccessful uses of the chmod, fchmod, and fchmodat system calls. - Fail
### V-270787 - Ubuntu 24.04 LTS must generate audit records for successful/unsuccessful uses of the creat, open, openat, open_by_handle_at, truncate, and ftruncate system calls. - Fail
### V-270809 - Ubuntu 24.04 LTS must generate audit records for any successful/unsuccessful use of unlink, unlinkat, rename, renameat, and rmdir system calls. - Fail
chown, chmod, creat, ulink are commands and not callable functions in PI OS TRIXIE 

### V-274870 - Ubuntu 24.04 LTS must audit any script or executable called by cron as root or by any privileged user. - Fail
An error in the SCC code or unknow issue with PI OS implementation  

Results: Low Severity (CAT III)
===============================

### V-270645 - Ubuntu 24.04 LTS must not have the "systemd-timesyncd" package installed. - Fail
Needs to be researched
### V-270658 - Ubuntu 24.04 LTS audit event multiplexor must be configured to offload audit logs onto a different system or storage media from the system being audited. - Fail
Needs to be configured/researched
### V-270690 - Ubuntu 24.04 LTS must automatically lock an account until the locked account is released by an administrator when three unsuccessful logon attempts have been made. - Fail
For Platform IT systems you rarely have user accounts.  You have a single administrative account, and you have the root account and root is locked.  Only sudo to root available. Locking after 3 failed logons would in general *brick* the system.  The alternative is to boot to single user mode if available and change the password.  The mitigation is PKI based logon which significantly reduces the likelihood of brute force logon.  Multiple Admin Accounts and Multiple PKI accounts are subject to further exploration.  It is out of scope but would fall under and extended set of enterprise PKI requirements.
### V-270734 - Ubuntu 24.04 LTS must be configured such that Pluggable Authentication Module (PAM) prohibits the use of cached authentications after one day. - Fail
Requires full enterprise PKI implementation with CA and revocation checking. Out of scope
### V-270751 - Ubuntu 24.04 LTS must compare internal information system clocks at least every 24 hours with an authoritative time server. - Fail
Needs to be configured/researched
### V-270752 - Ubuntu 24.04 LTS must synchronize internal information system clocks to the authoritative time source when the time difference is greater than one second. - Fail
Needs to be configured/researched
