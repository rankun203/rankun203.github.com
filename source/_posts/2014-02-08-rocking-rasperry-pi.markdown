---
layout: post
title: "Rocking Rasperry Pi"
date: 2014-02-08 15:55:37 +0800
comments: true
categories: [linux, RasperryPi]
---

##Keep in mind
- Use `sudo nmap -sP -T4 10.0.30.1-254` to detect connected devices.
- Then use `sudo nmap -v -A -T4 10.0.30.1` get all opened port and services on this machine.
- Start a vnc server on raspi. `vncserver :1 -geometry 1200x700 -depth 24`
- apt update use goagent proxy. `sudo apt-get -o Acquire::http::proxy="http://10.42.0.1:8087/" update`
- Statistic folder size: `du -h --max-depth=1`

##View the video over mplayer
Install mplayer: `sudo apt-get install mplayer`

Rasperry Pi: `raspivid -t 999999 -o | omxplayer`

##Stream video over a network ([Official Doc](http://www.raspberrypi.org/camera))
Install related tool (both client & raspi): `sudo apt-get install mplayer netcat`

Some Linux : `nc -l -p 5001 | mplayer -fps 31 -cache 1024 -`
(Record on the other side: `nc -l -p 5001 | ffmpeg -r 31 -i - out.avi`)

Rasperry Pi: `raspivid -t 999999 -o - | nc 10.42.0.1 5001`

##Camera Error
```text
$ raspistill -o haha.jpg
mmal: mmal_vc_component_enable: failed to enable component: ENOSPC
mmal: camera component couldn't be enabled
mmal: main: Failed to create camera component
mmal: Failed to run camera app. Please check for firmware updates
```
Fixed by: [Kernels >= 3.10: w1_gpio destroys i2c bus 0, raspicam doesn't work anymore](https://github.com/raspberrypi/linux/issues/435)

##Connect to Wifi
1. ifconfig: Enable your wireless device.
2. iwlist: List the available wireless access points.
3. iwconfig: Configure your wireless connection.
4. dhclient: Get your IP address via dhcp.
5. `/etc/network/if-up.d/upstart`

```bash
iwlist wlan0 scan
sudo iwconfig wlan0 essid rk_mint key s:password123
sudo dhclient wlan0
```

##Load Camera to `/dev/video0` [HELP](http://www.linux-projects.org/modules/sections/index.php?op=viewarticle&artid=14)
```bash
uv4l --driver raspicam --auto-video_nr 
```

##Motion detect [HELP](http://www.linux-projects.org/modules/sections/index.php?op=viewarticle&artid=16)
```bash
LD_PRELOAD=/usr/lib/uv4l/uv4lext/armv6l/libuv4lext.so motion -c ./motion.conf
```
