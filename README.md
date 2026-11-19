# ESP32-CAM Camera Web Server

I used an AI Thinker ESP32-CAM to stream video to a browser over my local Wi-Fi. The board runs Espressif's Arduino `CameraWebServer` example, which serves the camera controls and video feed from the ESP32 itself.

## Hardware and tools

- AI Thinker ESP32-CAM with an OV2640 camera
- CH340 USB-to-serial adapter on Windows, detected as `COM4` for this setup
- Arduino IDE with the Espressif ESP32 board package
- A 2.4 GHz Wi-Fi network and a browser on the same local network

This is the same board I used for my LED Blink lab. [Hardware photo](evidence/photos/esp32cam-hardware.jpg)

## Setup

1. In Arduino IDE, select **AI Thinker ESP32-CAM** and the serial port for your board.
2. Open [`CameraWebServer.ino`](sketches/CameraWebServer/CameraWebServer.ino) in Arduino IDE. Keep it in the [`CameraWebServer`](sketches/CameraWebServer/) folder with its companion files.
3. The included `board_config.h` already selects `CAMERA_MODEL_AI_THINKER`, which sets the pin mapping for this board.
4. In `CameraWebServer.ino`, replace the default `ssid` and `password` placeholders in your local copy.
5. Upload the sketch and open Serial Monitor at **115200 baud**. After the board boots, look for `WiFi connected` and `Camera Ready!` followed by the camera's local address. If you opened Serial Monitor after boot, reset the board to see the startup messages again.
6. Open the reported HTTP address in a browser on the same network and select **Start Stream**.

Keep real Wi-Fi credentials in your local copy of the sketch. I ran the camera on my local network.

## What I verified

| Check | Evidence |
| --- | --- |
| The AI Thinker model was enabled and the sketch uploaded successfully. The upload reached 100% and passed hash verification. | [Board configuration and upload](evidence/screenshots/board-config-and-upload.png) |
| The board joined Wi-Fi and reported that the camera was ready. | [Serial Monitor output](evidence/screenshots/serial-camera-ready.png) |
| The browser displayed a camera frame at **XGA (1024 × 768)** with **Stop Stream** visible. | [Browser stream](evidence/screenshots/browser-stream.png) |

The browser also showed an **LED Intensity** slider. A follow-up test would be to raise it slightly during a stream and verify that the onboard white LED responds.

## References

- [Espressif's Arduino CameraWebServer example](https://github.com/espressif/arduino-esp32/tree/master/libraries/ESP32/examples/Camera/CameraWebServer)
- [Last Minute Engineers ESP32-CAM guide](https://lastminuteengineers.com/getting-started-with-esp32-cam/), which I followed for this lab
