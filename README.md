# TenDollarWebcam

This little project has two goals:
1. Be a little open source webcam (with so-so quality, but hey $10 and open source)
2. Serve as an example app for the [Micro-RTSP](https://github.com/geeksville/Micro-RTSP)
library.

![sample VLC view](/docs/camview.png "Sample VLC output")

These camera are _very_ cheap (< $10) and the ESP32 has a fair amount of horsepower
left over for other work.

![devboards](/docs/devpict.jpg "Typical ESP32-CAM boards")

# Supported boards

Virtually any OV2460 + ESP32 board should work.

For boards other than this list you might (probably not) need to change esp32cam_config
to use the GPIO assignments for your hardware.

I've tested the following boards with the stock config: [ex1](https://www.banggood.com/Geekcreit-ESP32-CAM-WiFi-+-Bluetooth-Camera-Module-Development-Board-ESP32-With-Camera-Module-OV2640--p-1394679.html?rmmds=myorder&cur_warehouse=CN), [ex2](https://www.banggood.com/TTGO-T-Journal-ESP32-Camera-Development-Board-OV2640-SMA-WiFi-3dbi-Antenna-0_91-OLED-Camera-Board-p-1379925.html?rmmds=myorder&cur_warehouse=CN), [ex3](https://www.banggood.com/M5Stack-Official-ESP32-Camera-Module-Development-Board-OV2640-Camera-Type-C-Grove-Port-p-1333598.html?rmmds=myorder&cur_warehouse=CN).

## ESP32-CAM board special handling needed

This board is great in some ways: it has PSRAM (so can in theory capture might higher res images than SVGA) and it is cheap and tiny.  Two downsides:

* It has no built in USB port, so to program you'll need to use a USB serial adapter.  See docs for a photo of the proper pins.
* The GPIO assignments are different for the camera, so you'll need to define USEBOARD_AITHINKER

## TTGO-T board special handling needed

@drmocm contributed a config file for [this great board](https://www.aliexpress.com/item/TTGO-T-Camera-ESP32-WROVER-PSRAM-Camera-Module-ESP32-WROVER-B-OV2640-Camera-Module-0-96/32968683765.html).  It might be the current best choice because it
has an extra 8MB of RAM which makes it possible to use very high resolutions on the camera.  
You will need to #define USEBOARD_TTGO_T in ESP32-devcam.ino to get the proper bindings for this board.

# How to buy/install/run

This project uses the simple PlatformIO build system.  You can use the IDE, but for brevity
in these instructions I describe use of their command line tool.

1. Purchase one of the inexpensive ESP32-CAM modules from asia (see above).
2. Install [PlatformIO](https://platformio.org/).
3. Download this git repo and cd into it.
4. pio run -t upload (This command will fetch dependencies, build the project and install it on the board via USB)

The first time you run your device you'll need to use an Android or iOS app to give it
access to your wifi network.  See [instructions here](https://github.com/geeksville/AutoWifi/blob/master/README.md).

At this point your device should be happily serving up frames.  Either via
a web-browser at http://yourdeviceipaddr or more interestingly via a standard
RTSP video stream.  If your device has an LCD screen it will be showing the IP address and boot messages
to that screen.

To see the RTSP stream use the client of your choice, for example you can use VLC
as follows:
```
vlc -v rtsp://yourdevipaddr:8554/mjpeg/1
```

Note: an older version of these instructions/code had you manually place your
wifi keys into the source code.  That code is now commented out, in favor of [AutoWifi](https://github.com/geeksville/AutoWifi).
