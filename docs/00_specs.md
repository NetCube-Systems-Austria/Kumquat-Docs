# Kumquat Features and Specifications

## Overview

The Kumquat is a versatile embedded system designed for a wide range of applications. Built around the Allwinner V3s System-On-Chip, it offers powerful processing capabilities and a variety of connectivity options.

## Features

### Processor
- The Kumquat features the Allwinner V3s System-On-Chip, boasting an ARM Cortex-A7 @ 1.2GHz with NEON and VFPv4 extensions for enhanced performance.

### Memory
- DDR2 Memory: The Kumquat contains 64MB of DDR2 memory with up to 400MHz clock speed, ensuring smooth operation and efficient multitasking.

### Connectivity
- Ethernet: Equipped with a 10/100 Mbps Ethernet port, the Kumquat provides reliable wired network connectivity.
- USB: Multiple USB ports are available, including a USB-C Dual Role port and a console interface over a second USB-C port.
- Audio: The Kumquat features audio out and microphone in ports, enabling audio input and output functionalities.
- Isolated CAN-FD: Integrated isolated CAN-FD support for communication in industrial environments.
- WiFi and Bluetooth: The Kumquat utilizes an ESP32 module over SDIO for WiFi and Bluetooth connectivity.

### Storage
- SPI Flash: The Kumquat includes an 8MB SPI flash for bootloader and user code storage, ensuring quick and efficient boot times.
- I2C EEPROM: An I2C EEPROM is provided for storing MAC addresses and user data.
- SDIO Connector: The Kumquat offers an SDIO connector for attaching eMMC or SD-Card storage devices.

### IOs and Relays
- IOs: The Kumquat features 8 12/24V IOs, each capable of supplying a maximum of 500mA. The logic levels are auto-detected depending on the power supply, with a total board limit of 3A including the SoC.
- Relays: Equipped with 4 relays in normally open configuration, capable of switching a resistive load of up to 1A at 30VDC and up to 0.3A at 125VAC.

### RTC and Power
- RTC: The Kumquat includes a Real-Time Clock (RTC) with external battery support, ensuring accurate timekeeping even in the absence of power.

### Expansion
- QWIIC Connectors: The Kumquat features QWIIC connectors for easy integration with external I2C devices, enabling rapid prototyping and expansion.

## Operating System
- The Kumquat runs on Buildroot Linux with Mainline Linux kernel and U-Boot as bootloader, providing a stable and customizable operating environment.

## Supported Programming Languages
- Recommended programming languages for the Kumquat include C, C++, and Python3. However, other languages can also be used based on project requirements and developer preference.

## Specifications

- Processor: Allwinner V3s SoC with ARM Cortex-A7 @ 1.2GHz
- Memory: 64MB DDR2 with up to 400MHz clock speed
- Connectivity:
    - Ethernet: 10/100 Mbps
    - USB: USB-C Dual Role, Console over USB-C
    - Audio: Audio Out, Microphone In
    - CAN-FD: Isolated CAN-FD
    - WiFi/Bluetooth: ESP32 module over SDIO
- Storage:
    - SPI Flash: 8MB for bootloader and user code
    - I2C EEPROM: For MAC addresses and user data
    - SDIO Connector: For eMMC or SD-Card
- IOs and Relays:
    - IOs: 8x 12/24V IOs, auto-detect logic levels, max 500mA each, total 3A for board
    - Relays: 4x normally open, max 1A at 30VDC, max 0.3A at 125VAC
- RTC: With external battery support
- Expansion: QWIIC connectors for external I2C devices

## Applications

The Kumquat is suitable for a wide range of applications, including but not limited to:

- Industrial Automation
- Home Automation
- IoT (Internet of Things) Projects
- Robotics
- Embedded Systems Development

## Conclusion

With its robust features and specifications, the Kumquat offers a reliable and flexible platform for various projects and applications. Whether you're a hobbyist, developer, or professional, the Kumquat provides the tools you need to bring your ideas to life.