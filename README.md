# TenDollarWebcam

This little project has two goals:
1. Be a little open source webcam (with so-so quality, but hey $10 and open source)
2. Serve as an example app for the [Micro-RTSP](https://github.com/geeksville/Micro-RTSP)
library.

![sample VLC view](/docs/camview.png "Sample VLC output")

These camera are _very_ cheap (< $10) and the ESP32 has a fair amount of horsepower
left over for other work.

![devboards](/docs/devpict.jpg "Typical ESP32-CAM boards")

# How to buy/install/run

This project uses the simple PlatformIO build system.  You can use the IDE, but for brevity
in these instructions I describe use of their command line tool.

1. Purchase one of the inexpensive ESP32-CAM modules from asia. [ex1](https://www.banggood.com/Geekcreit-ESP32-CAM-WiFi-+-Bluetooth-Camera-Module-Development-Board-ESP32-With-Camera-Module-OV2640--p-1394679.html?rmmds=myorder&cur_warehouse=CN), [ex2](https://www.banggood.com/TTGO-T-Journal-ESP32-Camera-Development-Board-OV2640-SMA-WiFi-3dbi-Antenna-0_91-OLED-Camera-Board-p-1379925.html?rmmds=myorder&cur_warehouse=CN), [ex3](https://www.banggood.com/M5Stack-Official-ESP32-Camera-Module-Development-Board-OV2640-Camera-Type-C-Grove-Port-p-1333598.html?rmmds=myorder&cur_warehouse=CN).
2. Install (PlatformIO)[https://platformio.org/].
3. Download this git repo and cd into it.
4. cp src/wifikeys_template.h src/wifikeys.h - and then edit wifikeys.h with your network info.
5. pio run -t upload (This command will fetch dependencies, build the project and install it on the board via USB)

At this point your device should be happily serving up frames.  Either via
a web-browser at http://<yourdeviceipaddr> or more interestingly via a standard
RTSP video stream.  If your device has an LCD screen it will be showing the IP address and boot messages
to that screen.

To see the RTSP stream use the client of your choice, for example you can use VLC
as follows:
```
vlc -v rtsp://<yourdevipaddr>:8554/mjpeg/1
```
