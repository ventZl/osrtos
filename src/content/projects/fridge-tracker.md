---
title: Fridge Tracker (鲜知贴)
summary: A low-power smart home solution for tracking food and household items using
  ESP32-C3/S3 microcontrollers and e-paper displays. The system features server-side
  image rendering to minimize hardware overhead and supports various tri-color and
  four-color display sizes.
slug: fridge-tracker
codeUrl: https://github.com/xueyouluo/fridge_tracker
siteUrl: https://xueyou-diy-lab.yummy-tulip-8164.chatgpt.site/
lastUpdated: '2026-07-17'
licenses:
- NOASSERTION
image: /202607/fridge_tracker_0.avif
rtos: freertos
libraries:
- sqlite
topics:
- 3d-printing
- arduino
- e-paper
- eink
- esp32
- expiration-reminder
- food-tracker
- iot
- mcp
- nodejs
- smart-home
- sqlite
isShow: true
createdAt: '2026-07-31T14:19:17+00:00'
updatedAt: '2026-07-31T14:19:17+00:00'
---

The Fridge Tracker (鲜知贴) is a sophisticated, source-available project designed to bring order to household inventory management. By combining the low-power benefits of e-paper displays with the versatility of the ESP32 microcontroller, it provides a persistent, high-visibility reminder of what’s in your fridge, when it expires, and where it’s stored. 

### Technical Architecture

One of the most compelling aspects of this project is its architectural approach to rendering. Instead of forcing the ESP32 to handle complex font rendering and layout logic—tasks that are notoriously memory-intensive on microcontrollers—the Fridge Tracker offloads the heavy lifting to a Node.js server. The server generates the actual image frames (PNG or raw binary) tailored to the specific screen resolution and color depth. The ESP32 then functions as a thin client: it wakes up, downloads the pre-rendered frame, and pushes it directly to the display via SPI. This design allows for beautiful typography and complex UI layouts without requiring high-end embedded hardware.

### Hardware and Efficiency

The firmware is optimized for long-term battery operation. The ESP32 follows a strict power-management cycle: it wakes up at user-defined intervals, connects to Wi-Fi, and checks for updates. By utilizing ETag headers, the device can determine if the content has changed since the last sync. If the data is identical, the device skips the power-hungry screen refresh and immediately returns to deep sleep. 

The project supports a range of hardware, including the cost-effective ESP32-C3 Super Mini and the more robust ESP32-S3. Display support is equally flexible, covering 4.2-inch tri-color (Black/White/Red) panels and larger 3.97-inch or 7.5-inch four-color (Black/White/Yellow/Red) e-paper modules.

### User Experience and Provisioning

To ensure the device is easy to set up without hardcoding credentials, the firmware includes a captive portal for Wi-Fi provisioning. Upon its first boot, the device creates a local Wi-Fi hotspot named `XianZhiTie-xxxxxx`. Users can connect via a smartphone to configure their home network settings, the server address, and a unique pairing code. 

On the software side, the project provides a mobile-friendly H5 interface for managing items. It automatically calculates expiry status, prioritizes items nearing their end-of-life, and supports categorization for snacks, medicines, and daily necessities. For advanced users, the system can integrate with OpenAI-compatible APIs, allowing AI agents to help query and manage household items through natural language.

### Comprehensive Ecosystem

The repository is a complete "one-stop-shop" for makers. It includes:
- **Firmware**: C++ code for ESP32-C3/S3 using the Arduino framework.
- **Server**: A Node.js backend using SQLite for data persistence and Playwright for server-side rendering.
- **Enclosures**: 3D-printable CAD designs (STEP and 3MF formats) for both 4.2-inch and 7.2-inch form factors.

Whether deployed via a public hosting service or a local NAS, the Fridge Tracker offers a professional-grade DIY solution for modern home organization.
