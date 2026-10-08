# Lab 2: Smart Home

This lab uses three ESP32 boards connected through BLE mesh. The light sensor reports whether the room is dark. The switch controls a relay. The gateway has a webpage for turning the switch on and off.

## Programs

- `ch9/light_sensor`: TSL2561 light sensor
- `ch9/switch`: relay control
- `ch9/gateway`: Wi-Fi and web control

The shared code is in `ch9/common`. The sensor libraries are in `common/esp-idf-lib/components`. Keep these folders together.

## Build

Install PlatformIO in VS Code. Open one program folder and click Build. No board is needed to compile. The projects use Espressif 32 version 7.0.1 and ESP-IDF.

Before uploading the gateway, copy `ch9/gateway/include/wifi_config.example.h` to `wifi_config.h` in the same folder. Put your Wi-Fi name and password in the copy. Git ignores `wifi_config.h`. If the copy is missing, the gateway still builds with placeholder values but cannot connect to your Wi-Fi.

## Progress

All three programs compiled in the original development folder on October 8, 2026. They have not been uploaded or tested on hardware yet. The gateway build used temporary Wi-Fi values.

## Source

The starter code comes from Chapter 9 of Packt's *Internet of Things with ESP32*: https://github.com/PacktPublishing/Internet-of-Things-with-ESP32/tree/main/ch9

The original license and the sensor library licenses are included. The compatibility fixes update the old FreeRTOS tick name, enable the BLE mesh server models, and update the Wi-Fi interface name.
