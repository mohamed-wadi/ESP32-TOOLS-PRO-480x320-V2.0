# ESP32-TOOLS-PRO-480x320-V2.0

Multi-tool firmware for ESP32 Dev Module with 480x320 TFT SPI display. This V2.0 version adds real support for external IR and CC1101 modules, new WiFi/BLE tools, saveable IR capture and replay, sub-GHz RF analysis, and a more polished interface for personal lab use.

> Use this firmware only on your own networks, your own devices, and environments where you have authorization. Several features can scan, transmit, interfere with, or copy signals. The purpose of this project is learning, diagnostics, and personal lab use.

[![GitHub](https://img.shields.io/badge/GitHub-pepeangell5-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/pepeangell5)
[![Web Flasher](https://img.shields.io/badge/Web%20Flasher-Install%20Firmware-00C853?style=for-the-badge&logo=esphome&logoColor=white)](https://pepeangell5.github.io/ESP32-TOOLS-PRO-480x320-V2.0/)
[![Instagram](https://img.shields.io/badge/Instagram-pepeangelll-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/pepeangelll)
[![Facebook](https://img.shields.io/badge/Facebook-ESP32Tools-1877F2?style=for-the-badge&logo=facebook&logoColor=white)](https://www.facebook.com/esp32tools/)

## Table of Contents

- [What changed from V1.0](#what-changed-from-v10)
- [Target Hardware](#target-hardware)
- [Gallery](#gallery)
- [Firmware Screenshots](#firmware-screenshots)
- [Navigation](#navigation)
- [Main Features](#main-features)
  - [WiFi Tools](#wifi-tools)
  - [Radio Tools](#radio-tools)
  - [Signal Tools / IR](#signal-tools--ir)
  - [CC1101 Tools](#cc1101-tools)
  - [Bluetooth Tools](#bluetooth-tools)
  - [System Tools](#system-tools)
  - [Web Dashboard](#web-dashboard)
- [Components Used](#components-used)
  - [Component Images](#component-images)
  - [Full Wiring Diagrams](#full-wiring-diagrams)
  - [Reference Pinouts](#reference-pinouts)
  - [Connection Table](#connection-table)
  - [Shared SPI Bus](#shared-spi-bus)
  - [TFT Display 480x320](#tft-display-480x320)
  - [nRF24L01 #1](#nrf24l01-1)
  - [nRF24L01 #2](#nrf24l01-2)
  - [M5Stack IR Unit](#m5stack-ir-unit)
  - [CC1101](#cc1101)
  - [Buttons](#buttons)
  - [Visual Wiring Diagram](#visual-wiring-diagram)
  - [Quick Pin Map](#quick-pin-map)
- [Web Flasher](#web-flasher)
- [Build and Upload with PlatformIO](#build-and-upload-with-platformio)
- [Known Limitations](#known-limitations)
- [Credits](#credits)
- [Networks and Links](#networks-and-links)

## What Changed from V1.0

- Support for M5Stack IR Unit with capture, replay, signal saving, and virtual controls.
- Support for CC1101 sub-GHz module inside Radio Tools > CC1101.
- Renewed Jammer in Radio Tools for 2.4 GHz testing with dual nRF24L01.
- New BT Jammer inside Bluetooth Tools for educational 2.4 GHz sweep in personal lab.
- New WiFi tools: Channel Scan, WiFi Radar, and WiFi Direction Finder.
- New BLE Device Radar with RSSI tracking, estimated proximity, and clean details.
- New BLE Inspector to view manufacturer, type, appearance, and services.
- iPhone Remote / BLE HID experimental for testing with your own devices.
- Updated splash screen with cleaner text animation and BWifiKill branding.
- Menus with less flickering, cursor remembered on return, and clearer diagnostic screens.
- Pin documentation for soldering additional hardware without guessing.

[Back to top](#table-of-contents)

## Target Hardware

- Classic ESP32 Dev Module.
- 480x320 TFT SPI display with ILI9488 driver.
- 2 nRF24L01 modules for 2.4 GHz tools.
- M5Stack IR Unit with infrared receiver and transmitter.
- CC1101 sub-GHz module.
- 3 physical buttons: UP, OK, and DOWN.
- Cables, soldering, headers, and common GND for all modules.

The RF433T/RF433R modules are not included in this version because the CC1101 better covers sub-GHz work and allows more software diagnostics.

[Back to top](#table-of-contents)

## Gallery

| View | Image |
|------|-------|
| Finished device | |
| Front view | |
| Side view | |
| Internal view / assembly | |

[Back to top](#table-of-contents)

## Firmware Screenshots

| Menu | Image |
|------|-------|
| Splash | |
| Main menu | |
| WiFi Tools | |
| WiFi scanner / channels | |
| Radio Tools | |
| Bluetooth Tools | |
| Packet Monitor | |
| System Tools | |
| Screensaver | |

[Back to top](#table-of-contents)

## Navigation

- **UP**: scroll up or change value.
- **DOWN**: scroll down or change value.
- **OK**: enter, select, capture, or execute action.
- **OK (held)**: go back, cancel, or exit the current screen.
- Submenus remember the last selected option when returning.

[Back to top](#table-of-contents)

## Main Features

### WiFi Tools

- **WiFi Scanner**: scans nearby 2.4 GHz WiFi networks and shows SSID, BSSID, channel, RSSI, frequency, and security.
- **Channel Scan**: groups networks by channel, shows how many networks are on each channel, and allows opening the AP list per channel.
- **WiFi Radar**: lets you choose an AP and track it by RSSI, proximity percentage, peak, trend, and history.
- **WiFi Direction Finder**: measures RSSI by sectors to estimate from which direction a network is strongest.
- **WiFi Config**: connects the ESP32 to a network using a virtual keyboard and saves credentials to NVS.
- **Beacon Spam**: emits test beacons for controlled lab use.
- **Deauther**: WiFi testing tool for authorized environments.
- **Evil Portal**: educational captive portal to demonstrate phishing flows in a personal lab.
- **Probe Sniffer**: observes nearby WiFi probes and shows detected activity.
- **KARMA Attack**: educational mode to understand responses to probes and insecure associations.

> **Important limitation**: The classic ESP32 only works with 2.4 GHz WiFi. It cannot scan 5 GHz networks.

### Radio Tools

- **Jammer**: renewed mode for 2.4 GHz testing in a personal lab. Lets you choose a WiFi channel, start/stop with OK, and uses both nRF24L01 modules when available.
- **Radio Scanner**: visual 2.4 GHz analyzer with spectrum, activity per channel, and waterfall views.
- **Signal Tools**: IR tools and basic pin diagnostics.
- **CC1101**: dedicated sub-GHz menu with diagnostics, spectrum, monitor, finder, and RF analysis.

### Signal Tools / IR

- **Hardware Diag**: shows pins, SPI status, RX levels, and overall hardware status.
- **Input Monitor**: shows activity on IR RX and CC1101 GDO0 to validate wiring.
- **IR Raw Capture**: captures raw signals from infrared remotes.
- **IR Replay**: replays the last capture using 38 kHz IR carrier.
- **IR TX Test**: emits three IR flashes to validate the transmitter using a phone camera.
- **Saved Captures**: saves IR captures with a name, loads, replays, renames, or deletes them.
- **IR Remotes**: creates virtual remotes with buttons pointing to saved captures.
- **IR Analyzer**: live IR activity detector with IDLE, FRAME, REPEAT, and NOISE states.
- **Protocol Scan**: attempts to classify the signal as NEC, Samsung, LG, Sony, Panasonic, RC5, RC6, or RAW.
- **IR Sniffer**: records live IR events with protocol, code, bits, duration, and repeats.
- **Night IR**: detects pulsed/modulated IR activity from remotes, IR LEDs, sensors, or cameras with pulsed IR.
- **IR Proximity**: experimental IR bounce test. Does not measure real distance; heavily depends on physical mounting.

> **IR Notes:**
> - Many mini-splits/air conditioners use long codes with full state. Power up, power down, increase temperature, and decrease temperature may be completely different captures.
> - The demodulated IR receiver does not measure real analog intensity or exact carrier frequency. The bars represent detected activity, not precise optical power.
> - For reliable captures, aim the remote directly at the receiver and avoid strong IR light nearby.

### CC1101 Tools

- **Hardware Diag**: verifies SPI communication, PARTNUM, VERSION, MARCSTATE, RSSI, LQI, and GDO0 level.
- **Spectrum Scan**: sweeps common bands 315, 433, 868, and 915 MHz to view RSSI peaks.
- **Waterfall**: historical view of RF activity by frequency.
- **Frequency Mon**: monitors a fixed frequency such as 315.00, 390.00, 433.92, 868.35, or 915.00 MHz.
- **Freq Finder**: calibrates noise and automatically searches for the peak of a sub-GHz signal.
- **Brute Search**: broad search to find candidate activity.
- **Code Check**: compares several presses to see if a signal appears fixed or rolling.
- **RF Analyzer**: shows pulses, total duration, short/long averages, OOK/ASK type, and signature/hash.
- **RF Raw View**: captures and draws the signal as bars/pulses to compare buttons.
- **RF Live**: live detector with frequency, peak RSSI, event counter, and last activity.
- **Lab Replay**: RF OOK/ASK replay for your own fixed-code devices and lab testing only.
- **Test Beacon**: short test transmission to validate RF output in a controlled environment.

> **CC1101 Notes:**
> - 433.92 MHz and 434 MHz normally refer to the same practical range. Many remotes are advertised as 434 MHz even though they operate near 433.92 MHz.
> - The frequency meter is approximate. It does not replace a professional spectrum analyzer.
> - Do not use RF replay on cars, garage doors, alarms, locks, or third-party systems. Many use rolling codes and must not be copied or tested outside a personal lab.

### Bluetooth Tools

- **BLE Device Radar**: scans BLE, shows name, MAC, RSSI, manufacturer/type, and allows tracking a target with history.
- **BLE Inspector**: enhanced scanner with classification by manufacturer, appearance, device type, and services.
- **iPhone Remote**: experimental BLE HID mode for pairing/basic control on your own devices.
- **BLE Spam**: educational BLE testing in lab.
- **BT Disruptor**: controlled lab Bluetooth testing.
- **BT Jammer**: 2.4 GHz sweep with dual nRF24L01 for short-range educational testing in a personal environment.

### System Tools

- **Settings**: device configuration and saved options.
- **System Info**: memory, firmware, and ESP32 status information.
- **Clock & Weather**: clock/weather with virtual keyboard for setup.
- **Web Dashboard**: creates the ESP32-TOOLS-PRO AP with password admin1234 and opens a web panel at http://192.168.4.1.
- **About**: project information.

## Web Dashboard

Phase 1 of the web dashboard is activated from System > Web Dashboard. When entered, the ESP32 creates its own AP:

```
SSID: ESP32-TOOLS-PRO
PASS: admin1234
URL : http://192.168.4.1
```

Features available in phase 1:

- General dashboard with uptime, free heap, connected clients, and main pins.
- Quick diagnostics of IR RX and CC1101 GDO0 levels.
- List of saved IR captures with replay, rename, and delete.
- CC1101 monitor by preset frequency: 315.00, 390.00, 433.92, 868.35, and 915.00 MHz.
- WiFi Tools from browser:
  - **WiFi Scanner**: network list, channel, RSSI, security, and BSSID.
  - **Channel Scan**: summary by channel and 2.4 GHz network table.
  - **WiFi Radar**: select an AP and track it by RSSI/proximity.
  - **Direction Finder**: measures front, right, back, and left to suggest the strongest direction.
  - **Beacon Spam**: web-controlled demo with lab SSIDs, fixed dashboard channel, start/stop button, and auto-stop.
  - Deauther, Evil Portal, Probe Sniffer, and KARMA Attack appear as LOCAL ONLY for use from the device screen.

> The dashboard does not execute functions that take full control of WiFi such as Deauther, Evil Portal, KARMA, or jamming. This is intentional to avoid conflicts with the dashboard AP and keep it stable.

[Back to top](#table-of-contents)

## Components Used

| Component | Description | Recommended Voltage | Notes |
|-----------|-------------|---------------------|-------|
| ESP32 Dev Module | Main microcontroller | USB/5V on board | GPIO logic at 3.3V |
| TFT 480x320 ILI9488 SPI | Main display | Depends on module, commonly 5V or 3.3V | SPI signals at 3.3V |
| nRF24L01 #1 | Primary 2.4 GHz radio | 3.3V | Do not power at 5V |
| nRF24L01 #2 | Secondary 2.4 GHz radio | 3.3V | Capacitor recommended near VCC/GND |
| M5Stack IR Unit | Infrared receiver + transmitter | 5V | Wiring verified with OUT on GPIO26 and IN on GPIO34 |
| CC1101 | Sub-GHz radio for 315/433/868/915 MHz | 3.3V | Do not power at 5V |
| UP/OK/DOWN Buttons | Firmware navigation | GPIO to GND | Uses internal INPUT_PULLUP |

## Component Images

| Component | Image |
|-----------|-------|
| ESP32 Dev Module | |
| ILI9488 480x320 Display | |
| nRF24L01 Modules | |
| nRF24L01 | |
| CC1101 | |
| Antenna | |
| M5Stack IR Unit | |
| IR Unit view 2 | |
| Buttons | |
| Battery | |
| TP4056 | |
| Step-up | |
| Switch | |
| PCB board / assembly | |

## Full Wiring Diagrams

These diagrams show the wiring by blocks to make it easier to solder and review the assembly without a single cluttered image.

**Display TFT and buttons**

**nRF24L01 modules**

**CC1101 and IR Remote**

## Reference Pinouts

| Module | Pinout |
|--------|--------|
| nRF24L01 PA + LNA | |
| CC1101 | |

[Back to top](#table-of-contents)

## Connection Table

All modules must share GND with the ESP32. Do not connect any 3.3V module to 5V.

### Shared SPI Bus

| Signal | ESP32 GPIO | Used by |
|--------|-----------|---------|
| SCK | GPIO18 | TFT, nRF24 #1, nRF24 #2, CC1101 |
| MOSI | GPIO23 | TFT, nRF24 #1, nRF24 #2, CC1101 |
| MISO | GPIO19 | nRF24 #1, nRF24 #2, CC1101 |

Each SPI module has its own CS/CSN pin, so they can share SCK/MOSI/MISO.

### TFT Display 480x320

| TFT Pin | ESP32 GPIO | Note |
|---------|-----------|------|
| CS | GPIO5 | TFT chip select |
| RST | GPIO4 | TFT reset |
| DC / RS | GPIO22 | Data/Command |
| LED / BL | GPIO13 | Backlight |
| SCK / CLK | GPIO18 | Shared SPI |
| MOSI / SDI | GPIO23 | Shared SPI |
| MISO / SDO | Not used by TFT | Firmware defines TFT MISO as -1 |
| VCC | Depends on module | Check your display: some accept 5V, others 3.3V |
| GND | GND | Common ground |

### nRF24L01 #1

| nRF24 Pin | ESP32 GPIO | Note |
|-----------|-----------|------|
| CE | GPIO27 | Radio #1 control |
| CSN | GPIO14 | Radio #1 chip select |
| SCK | GPIO18 | Shared SPI |
| MOSI | GPIO23 | Shared SPI |
| MISO | GPIO19 | Shared SPI |
| VCC | 3.3V | Do not use 5V |
| GND | GND | Common ground |

### nRF24L01 #2

| nRF24 Pin | ESP32 GPIO | Note |
|-----------|-----------|------|
| CE | GPIO17 | Radio #2 control |
| CSN | GPIO16 | Radio #2 chip select |
| SCK | GPIO18 | Shared SPI |
| MOSI | GPIO23 | Shared SPI |
| MISO | GPIO19 | Shared SPI |
| VCC | 3.3V | Do not use 5V |
| GND | GND | Common ground |

### M5Stack IR Unit

| IR Module Pin | ESP32 GPIO | Firmware Function | Note |
|--------------|-----------|-------------------|------|
| OUT | GPIO26 | IR_TX_PIN | ESP32 output to module IR transmitter |
| IN | GPIO34 | IR_RX_PIN | ESP32 input from module IR receiver |
| 5V | 5V | Power | M5Stack IR module works at 5V |
| GND | GND | Common ground | Ground sharing is mandatory |

GPIO34 is input-only, which is why it is used to receive IR. GPIO26 is used to transmit.

### CC1101

| CC1101 Pin | ESP32 GPIO | Firmware Function | Note |
|------------|-----------|-------------------|------|
| CSN / CS | GPIO21 | CC1101_CSN_PIN | CC1101 chip select |
| SCK | GPIO18 | Shared SPI | SPI clock |
| MOSI / SI | GPIO23 | Shared SPI | Data from ESP32 to CC1101 |
| MISO / SO | GPIO19 | Shared SPI | Data from CC1101 to ESP32 |
| GDO0 | GPIO35 | CC1101_GDO0_PIN | RF RX/edges input |
| GDO2 extra | GPIO15 | CC1101_TX_DATA_PIN | Optional jumper for Lab Replay |
| VCC | 3.3V | Power | Do not use 5V |
| GND | GND | Common ground | Ground sharing is mandatory |

The extra GDO0 -> GPIO15 jumper is only needed for Lab Replay testing. You can leave it out if you will only use diagnostics, monitor, finder, analyzer, and raw view.

### Buttons

| Button | ESP32 GPIO | Wiring |
|--------|-----------|--------|
| UP | GPIO32 | Button between GPIO32 and GND |
| OK | GPIO33 | Button between GPIO33 and GND |
| DOWN | GPIO25 | Button between GPIO25 and GND |

Buttons use internal pull-up. When pressed, the pin goes LOW.

[Back to top](#table-of-contents)

## Visual Wiring Diagram

[Back to top](#table-of-contents)

## Quick Pin Map

```
ESP32 GPIO18 -> Shared SPI SCK
ESP32 GPIO23 -> Shared SPI MOSI
ESP32 GPIO19 -> Shared SPI MISO

ESP32 GPIO5  -> TFT CS
ESP32 GPIO4  -> TFT RST
ESP32 GPIO22 -> TFT DC
ESP32 GPIO13 -> TFT Backlight

ESP32 GPIO27 -> nRF24 #1 CE
ESP32 GPIO14 -> nRF24 #1 CSN
ESP32 GPIO17 -> nRF24 #2 CE
ESP32 GPIO16 -> nRF24 #2 CSN

ESP32 GPIO26 -> IR OUT / TX
ESP32 GPIO34 -> IR IN / RX

ESP32 GPIO21 -> CC1101 CSN
ESP32 GPIO35 -> CC1101 GDO0 RX
ESP32 GPIO15 -> CC1101 GDO0 TX optional for Lab Replay

ESP32 GPIO32 -> Button UP to GND
ESP32 GPIO33 -> Button OK to GND
ESP32 GPIO25 -> Button DOWN to GND
```

[Back to top](#table-of-contents)

## Web Flasher

Direct flashing from browser:

https://pepeangell5.github.io/ESP32-TOOLS-PRO-480x320-V2.0/

The page uses ESP Web Tools and these files from the repo:

- **index.html**: flashing page with ESP Web Tools.
- **manifest.json**: manifest used by ESP Web Tools.
- **assets/Firmware/firmware-merged.bin**: complete binary for flashing from offset 0x0.
- **assets/Firmware/firmware.bin**: compiled application.
- **assets/Firmware/bootloader.bin**: bootloader.
- **assets/Firmware/partitions.bin**: partition table.

Target repo:

https://github.com/pepeangell5/ESP32-TOOLS-PRO-480x320-V2.0

[Back to top](#table-of-contents)

## Build and Upload with PlatformIO

Build:

```bash
pio run
```

Upload to ESP32:

```bash
pio run -t upload --upload-port COM3
```

If the upload fails with a boot/serial error, hold the BOOT button when starting the upload and release it when PlatformIO begins writing.

[Back to top](#table-of-contents)

## Known Limitations

- WiFi is 2.4 GHz only because the classic ESP32 does not have a 5 GHz radio.
- The CC1101 gives approximate RSSI/frequency readings; it is not a professional spectrum analyzer.
- IR Proximity is experimental and may stay at NONE depending on the angle and physical bounce.
- Air conditioners typically use long signals with full state; save each function separately.
- Jammer, BT Jammer, BLE Spam, BT Disruptor, Deauther, KARMA, and Beacon Spam are lab functions. They can degrade nearby communications and must only be used with authorization.
- Lab Replay RF is intended for bulbs, plugs, or your own fixed-code devices. It is not for vehicles, alarms, locks, or garage doors.
- RF433T/RF433R modules are excluded from V2.0.

[Back to top](#table-of-contents)

## Credits

Project created and tested by PepeAngell for ESP32-TOOLS-PRO-480x320-V2.0.

[Back to top](#table-of-contents)

## Networks and Links

- **GitHub**: github.com/pepeangell5
- **Web Flasher**: pepeangell5.github.io/ESP32-TOOLS-PRO-480x320-V2.0
- **Instagram**: @pepeangelll
- **Facebook**: ESP32Tools

[Back to top](#table-of-contents)

[Back to top](#table-of-contents)
