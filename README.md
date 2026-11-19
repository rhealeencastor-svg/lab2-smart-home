# Lab 2 Smart Home

Three ESP32 boards form a BLE Mesh network. The light sensor measures lux, the switch drives a relay, and the Wi-Fi gateway serves an ON/OFF page.

## What you need

- An ESP32-S3 DevKitC-1 for the gateway and two ESP32-WROOM development boards for the sensor and switch
- A TSL2561 light sensor breakout, a relay module with a 3.3 V-compatible input, breadboards, jumpers, and USB data cables
- An indicator LED and 220 Ω resistor per board for identification during provisioning
- VS Code with PlatformIO, a 2.4 GHz Wi-Fi network, and nRF Mesh on a phone

## Open and upload

Clone the whole repo. Open the matching folder in VS Code and plug in one board at a time.

| Folder | PlatformIO environment | Main connections |
| --- | --- | --- |
| `gateway/` | `esp32-s3-devkitc-1` | Wi-Fi and the ON/OFF page. Use the S3 COM/UART USB port when using GPIO19 as the indicator. |
| `light_sensor/` | `az-delivery-devkit-v4` | TSL2561 power at 3.3 V, common GND, SDA on GPIO21, SCL on GPIO22. |
| `switch/` | `az-delivery-devkit-v4` | GPIO4 to the compatible relay input and common GND. Power the relay at its rated voltage. |

The shared LED and mesh code and the sensor drivers are in `shared/`.

1. Before building the gateway, copy `gateway/include/wifi_config.example.h` to `gateway/include/wifi_config.h` and enter your Wi-Fi settings locally. Git ignores the local file.
2. Open a terminal in the selected project folder and run the matching command.

   ```bash
   # From gateway/
   pio run -e esp32-s3-devkitc-1 -t upload -t monitor

   # From light_sensor/ or switch/
   pio run -e az-delivery-devkit-v4 -t upload -t monitor
   ```

3. Check for `Lux:` in the sensor monitor and `sta ip:` in the gateway monitor.

## Test the lab

1. Power all three boards. Provision them in nRF Mesh on one network and bind the same app key to the models below.

   | Node | App key binding |
   | --- | --- |
   | Gateway | Generic OnOff Client |
   | Switch | Generic OnOff Client and Server |
   | Light sensor | Generic OnOff Server, publication set to All Nodes |

2. From a device on the gateway Wi-Fi network, open `http://` followed by the gateway IP from `sta ip:`. Try ON and OFF with the relay's load terminals empty for the first click test.
3. Cover the TSL2561, then uncover it or shine a light on it. Check that changes across 30 lux reach the switch.

Starter firmware adapted from [Chapter 9 of Packt's Internet of Things with ESP32](https://github.com/PacktPublishing/Internet-of-Things-with-ESP32/tree/main/ch9). The source and bundled drivers retain their licenses.
