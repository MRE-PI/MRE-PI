---
nav_order: 7
layout: default
title: Raw_Build
nav_enabled: true
---

dmesg | grep -i firmware
Increase swap to 1024

Build

wget https://raw.githubusercontent.com/Motion-Project/motion-packaging/master/buildplus.sh

sudo apt install autoconf automake autopoint build-essential pkgconf libtool libzip-dev libjpeg-dev git libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libavdevice-dev libopencv-dev libwebp-dev gettext libmicrohttpd-dev libmariadb-dev libcamera-dev libcamera-tools libasound2-dev libpulse-dev libfftw3-dev
sudo apt-get install libpq-dev libsqlite3-dev debhelper dh-autoreconf
sudo apt-get install libcamera-v4l2

sudo ./buildplus.sh

cd ~
git clone https://github.com/Motion-Project/motionplus.git
cd motionplus
autoreconf -fiv
./configure
make
sudo make install
