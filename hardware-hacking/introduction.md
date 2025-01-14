---
icon: info
---

# Introduction

Imagine owning an IoT device like a router, smart light, or Wi-Fi camera and wanting to investigate its security. Your first instinct might be to scan for open ports, services, or web server vulnerabilities. But what if these software-based attack vectors reveal nothing? Is the game over? Not at all! While the software might be secure, the hardware often tells a different story. Debug ports can be abused to gain root shells, firmware can be dumped from microchips, and communication lines can be sniffed to uncover sensitive data.

### Why Consider Hardware Hacking?

Hardware hacking offers a deeper layer of exploration beyond traditional software-based security testing. Devices often have physical interfaces and chips that store critical data, such as credentials or encryption keys, that attackers might exploit. Even if software vulnerabilities are absent, the hardware can often be a treasure trove of opportunities for bypassing security mechanisms.

By mastering hardware hacking, you can:

* Discover vulnerabilities that software tests cannot reveal.
* Extract valuable insights by dumping firmware or accessing memory directly.
* Understand and manipulate the low-level workings of IoT devices.

### What is the Goal of Hardware Hacking?

The primary goal of a hardware hacker is typically to gain full control of the device, escalating privileges and accessing sensitive data. For example:

* Interactive Access
  * Obtaining an administrative shell that allows full control of the device.
* [Firmware Extraction](../hardware-hacking/basics/firmware-extraction-methods.md)
  * Dumping the device's firmware, which contains all the code and secrets required for operation. This can reveal admin passwords, hardcoded credentials, or security flaws.
* Firmware Modification
  * Reflashing a device with modified firmware to bypass restrictions or gain privileged access.

### How Do We Start?

Check out the[ How to start](../introduction/how-to-start.md) guide, which give you guidance on what target device to choose (if you don't have one already), what tools are needed for beginners and how to approach hardware hacking in general.

After opening the device, the first step is identifying key hardware components and interfaces. In the [Board Analysis](reconnaissance/opened-device/board-analysis.md) we describe in detail how to identify each component and how we can abuse it. A short summary:

* Debug Interfaces (e.g., [UART](interface-interaction/uart/), [JTAG/SWD](interface-interaction/jtag-swd/))
  * These allow direct communication with the device, often providing admin-level access if unsecured.
* Memory Chips (e.g., [SPI Flash](interface-interaction/spi/), EEPROM)
  * &#x20;These store firmware and critical data, which can often be [extracted](interface-interaction/spi/extract-firmware-using-spi.md) and analyzed.
* Communication Lines (e.g.,[ I2C](interface-interaction/i2c.md), [SPI](interface-interaction/spi/), [UART](interface-interaction/uart/))
  * Sniffing these can reveal unencrypted data in transit, such as credentials or sensitive commands. This can be done by using a [logic analyzer](basics/tools/hardware-tools/logic-analyzer/).

Once the firmware or data is extracted, tools like [**binwalk**](basics/tools/software-tools/binwalk.md), [**Ghidra**](basics/tools/software-tools/ghidra.md), and **radare2** can help reverse-engineer the firmware, uncovering hardcoded secrets, encryption keys, or exploitable vulnerabilities.

### Next Steps

The content of this wiki has a top to button approach, so you can just follow the natural order of the content to start your deep dive into hardware hacking:

* [_**Basics**_](basics/)\
  Start by familiarizing yourself with essential hardware and software tools. Learn about devices like the **Bus Pirate**, **JTAG adapters**, and **logic analyzers**, as well as software like **Ghidra** and **binwalk**, which are critical for hardware hacking.
* [_**Reconnaissance**_](reconnaissance/)\
  Discover how to enumerate a device and identify hardware interfaces. This chapter focuses on understanding and locating **UART**, **JTAG**, and **SPI** interfaces. Begin your journey with the _Board Analysis_ section to learn how to inspect and analyze a device's hardware layout.
* [_**Interface Interaction**_](interface-interaction/)\
  Found a debugging interface like JTAG or UART? This chapter will teach you how to interact with it to extract data, dump firmware, and explore the internal workings of the device.
* [_**Bypassing Security**_](bypassing-security/)\
  Take your skills to the next level with advanced techniques for bypassing security mechanisms. Learn approaches to overcome challenges like read-out protections on chips and explore topics like **side-channel attacks** for deeper hardware penetration.
* [_**Analyze Firmware**_](analyze-firmware.md)\
  Once you’ve extracted firmware, this chapter guides you through analyzing it using tools like **binwalk** to uncover vulnerabilities, hardcoded secrets, and sensitive information.

