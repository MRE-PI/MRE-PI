##sudo nano /boot/config.txt
add dtoverlay=imx219 v2 Camera
add dtoverlay=imx477 HQ Camera
add dtoverlay=imx296 GS Camera
add dtoverlay=imx708 Cammera Module 3
##sudo apt install -y opensc
##sudo apt install libpam-pkcs11
##sudo apt install auditd
##sudo apt install ufw
##sudo apt install libpam-pwquality -y
##sudo apt install apparmor
##sudo apt install chrony

##sudo apt install opensc libpam-pkcs11 auditd ufw libpam-pwquality apparmor vlock aide chrony -y
##sudo apt install opensc-pkcs11 pcscd sssd libpam-sss

sudo apt install opensc-pkcs11 pcscd sssd libpam-sss opensc libpam-pkcs11 libfido2-1 libfido2-dev libfido2-doc fido2-tools yubikey-manager pcsc-tools libpcsclite1

Motion

 no--##sudo apt install ffmpeg libmariadb3 libpq5 libmicrohttpd12 -y

##sudo apt install ffmpeg python2 -y

##sudo apt install v4l-utils 


sudo apt install libmariadb3 libmicrohttpd12 libpq5 -y


 wget https://github.com/Motion-Project/motion/releases/download/release-4.6.0/bullseye_motion_4.6.0-1_armhf.deb

 dpkg -i bullseye_motion_4.6.0-1_armhf.deb


##sudo systemctl stop motion
##sudo systemctl disable motion
##sudo curl https://bootstrap.pypa.io/pip/2.7/get-pip.py --output get-pip.py
##sudo python2 get-pip.py
## sudo apt install python-dev-is-python2 python-setuptools libssl-dev libcurl4-openssl-dev libjpeg-dev zlib1g-dev libffi-dev libzbar-dev libzbar0 -y
##sudo pip install motioneye


##sudo apt update
Sudo apt upgrade if needed
