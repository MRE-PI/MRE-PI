---
nav_order: 2
layout: default
title: Raw_Build
parent: App Install
nav_enabled: true
---

dmesg | grep -i firmware  
Increase swap to 1024  

Build  
```markdown
wget https://raw.githubusercontent.com/Motion-Project/motion-packaging/master/buildplus.sh  
```
~~```markdown
~~sudo apt install autoconf automake autopoint build-essential pkgconf libtool libzip-dev libjpeg-dev git libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libavdevice-dev libopencv-dev libwebp-dev gettext libmicrohttpd-dev libmariadb-dev libcamera-dev libcamera-tools libasound2-dev libpulse-dev libfftw3-dev~~  
```~~
```markdown
sudo apt install openssl-provider-fips opensc libpam-pkcs11 auditd ufw libpam-pwquality apparmor vlock aide chrony libopencv-dev libcamera-dev libcamera-v4l2 libcamera-tools libavdevice-dev libmicrohttpd-dev libfftw3-dev libfftw3-double3 libmariadb-dev libmariadb3 mariadb-client mariadb-client-core mariadb-common mariadb-server autoconf automake autopoint build-essential pkgconf libtool libzip-dev libjpeg-dev git libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libwebp-dev gettext libasound2-dev libpulse-dev ffmpeg v4l-utils libswresample-dev nginx-common nginx-core libnginx-mod-rtmp -y  
```
```martdown
sudo apt install sssd libpam-sss libpam-cap ykcs11 yubikey-personalization yubikey-manager^  
```
~~```markdown
~~sudo apt-get install libcamera-v4l2~~
```~~
```markdown
sudo ./buildplus.sh  
```
cd ~  
```markdown
git clone https://github.com/Motion-Project/motionplus.git  
```
cd motionplus  
```markdown
autoreconf -fiv  
```
```markdown
./configure
```
make  
```markdown
sudo make install  
```
