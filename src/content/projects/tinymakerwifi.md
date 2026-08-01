---
title: TinyMakerWifi
summary: TinyMakerWifi is an enhanced firmware for the TinyMaker MSLA resin 3D printer
  that introduces WiFi connectivity, a web-based dashboard, and direct integration
  with PrusaSlicer. Built on the ESP32 platform using the Arduino framework and FreeRTOS,
  it features advanced resin tracking, power-loss recovery, and over-the-air (OTA)
  updates.
slug: tinymakerwifi
codeUrl: https://github.com/slibbinas/TinyMakerWifi
siteUrl: https://tinymakerwifi.com
version: v0.15.8
lastUpdated: '2026-07-30'
licenses:
- NOASSERTION
image: /202607/TinyMakerWifi_0.avif
rtos: freertos
libraries:
- platformio-platformio-core
topics:
- 3d-printer
- esp32
- firmware
- open-source-hardware
- platformio
- tinymaker
- wifi-module
isShow: true
createdAt: '2026-07-31T01:38:21+00:00'
updatedAt: '2026-07-31T01:38:21+00:00'
relatedProjects:
- klipper-esp32
- advanced-filament-sensor-for-elegoo-carbon-centauri
- sha2017-badge-firmware
- esp32-bus-expander
- ikedrybox-smart-3d-filament-dryer
- openspool
---

TinyMakerWifi is a modified and extended firmware for the open-source TinyMaker MSLA resin 3D printer. The project’s primary goal is to modernize the user experience by eliminating the need for manual SD card swapping, replacing it with seamless WiFi connectivity, OTA updates, and direct model uploads from popular slicing software like PrusaSlicer.


### Core Features and Capabilities

The firmware transforms the palm-sized printer into a fully networked device. On the first boot, it launches a captive portal for easy WiFi configuration from a smartphone, ensuring that no credentials need to be hardcoded. Once connected, the printer emulates the Prusa SL1 network protocol, allowing users to hit "Send to printer" directly within PrusaSlicer. The system automatically handles the unpacking of `.sl1` or `.zip` archives into the specific layer formats required by the hardware.

The on-device user interface has been significantly expanded. A new System menu provides access to WiFi information, firmware update tools, and advanced settings. These advanced controls include screen timeout adjustments, dry run modes, and sophisticated resin-tracking controls that monitor VAT levels to prevent mid-print failures. Users can also perform model management directly from the printer's screen, including deleting models or importing archives from an SD card without network access.

![TinyMaker WiFi — printer UI screens](/202607/TinyMakerWifi_1.avif)

### Advanced Resin and Power Management

One of the most technical additions is the resin usage estimation system. The firmware analyzes the pixel data of each layer to calculate the volume of resin required. It keeps a running estimate of the resin remaining in the VAT, offering low-resin warnings and an optional auto-pause feature for refills. 

For reliability, the project incorporates a robust power-loss recovery engine. By frequently checkpointing progress to the SD card, the printer can resume a print exactly where it left off after a power interruption. This recovery can be triggered either from the physical printer interface or remotely via the web dashboard. For maintenance, the firmware includes a built-in exposure calibration test that cures an 8-bar test strip, helping users dial in perfect settings without needing to slice external files.

### Web Dashboard and Remote Monitoring

The web dashboard provides a comprehensive interface for managing the printer from any browser. It includes an SD card manager, live print status with controls, and a device configuration tab. A standout feature is the real-time 3D progress render; the browser rebuilds the model's shape from the sliced layer images, showing the printed part filling up in color against a ghost outline of the remaining model. This rendering happens entirely on the client side, ensuring zero additional load on the printer's ESP32 microcontroller.

![TinyMakerWiFi web dashboard: live print status, controls and SD manager](/202607/TinyMakerWifi_5.avif)

Beyond simple control, the firmware supports modern automation ecosystems. It includes optional MQTT integration with Home Assistant auto-discovery, allowing users to monitor print states, resin levels, and remaining time as sensors. It also supports outbound notifications via Telegram, WhatsApp, or Discord webhooks to alert users when a print finishes or requires attention.

![Real dashboard screenshot while printing with live 3D progress](/202607/TinyMakerWifi_7.avif)

### Technical Architecture and Hardware

The project targets the stock TinyMaker electronics, which utilize the ESP32-WROOM-32E-N4 module. Despite the constraints of 4 MB of flash and no PSRAM, the firmware manages motor control, UV LED timing, a file system, and a web server simultaneously. It leverages the Arduino framework and the ESP-IDF `esp_timer` for hardware-level timing accuracy during curing cycles. 

The firmware is designed with safety in mind, utilizing a dual-partition OTA scheme that preserves the previous firmware version if an update fails. Developers can build the project using PlatformIO, with the ability to toggle network features entirely if a purely offline, original-style experience is desired.
