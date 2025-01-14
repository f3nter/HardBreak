---
icon: hand-wave
cover: >-
  https://images.unsplash.com/photo-1610878785620-3ab2d3a2ae7b?crop=entropy&cs=srgb&fm=jpg&ixid=M3wxOTcwMjR8MHwxfHNlYXJjaHw3fHxtaWNyb2NvbnRyb2xsZXJ8ZW58MHx8fHwxNzI4Mzk0NjM3fDA&ixlib=rb-4.0.3&q=85
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# HardBreak - Hardware Hacking Wiki

_**This page is a free and collaborative wiki about hardware hacking!**_

<figure><img src=".gitbook/assets/image (16).png" alt="" width="155"><figcaption><p>HardBreak Wiki</p></figcaption></figure>

The goal of HardBreak ([https://www.hardbreak.wiki/](https://www.hardbreak.wiki/)) is to collect knowledge about Hardware Hacking / IoT hacking in one place. There are many great blogs about Hardware Hacking, but it is a rather unpleasant experience to search through multiple blogs in different formats to find the information you need. HardBreak aims to organize all information in one accessible and easy-to-use platform.

## Discord

**🎉 We just launched our HardBreak Discord Server! 🎉**

Join us here 👉 [**https://discord.gg/AWVsKxJHvQ**](https://discord.gg/AWVsKxJHvQ)

If you:

* Want to discuss hardware hacking and IoT security
* Share the project you are working on
* Have feedback or requests for new content on our wiki

Come be a part of our growing community of hardware hackers⚡

{% hint style="success" %}
Hey! I’m Jonas Rosenberger, the creator of HardBreak. I’d love to hear your feedback or help out with any projects you’re working on. Feel free to reach out on [LinkedIn](https://www.linkedin.com/in/jonas-rosenberger-3276b1164/) or Discord (f\_3nter)!
{% endhint %}

## Overview

* [Introduction](introduction/how-to-start.md)
  * In this chapter we give you guidance on how to start hardware hacking:
    * What first target device to choose
    * Essential tools to start with
    * [Methodology](introduction/quickstart.md)
    * A hands on [Case Study](introduction/case-study-led-to-a-cve-update/general-case-study.md)
* [Hardware Hacking](hardware-hacking/introduction.md)
  * Top down approach to follow and investigate your device
    * [Basics](hardware-hacking/basics/) ([Hardware Tools](hardware-hacking/basics/tools/hardware-tools/), [Software](hardware-hacking/basics/tools/software-tools/) and [Common Hardware Components](hardware-hacking/basics/common-hardware-components.md))
  * [Reconnaissance](hardware-hacking/reconnaissance/) ([OSINT](hardware-hacking/reconnaissance/closed-device/osint-search-the-web.md), [Board Analysis](hardware-hacking/reconnaissance/opened-device/board-analysis.md))
  * [Interface Interaction](hardware-hacking/interface-interaction/):
    * Introduction to different protocols: e.g.,[UART](hardware-hacking/interface-interaction/uart/), [JTAG](hardware-hacking/interface-interaction/jtag-swd/jtag/), [SWD](hardware-hacking/interface-interaction/jtag-swd/swd.md), [SPI](hardware-hacking/interface-interaction/spi/), [I2C](hardware-hacking/interface-interaction/i2c.md)..
      * How to [Identify](hardware-hacking/interface-interaction/uart/uart-from-start-to-finish.md) and use those protocols
      * [extract firmware](hardware-hacking/interface-interaction/uart/extract-firmware-using-uart.md) using debug protocols
  * [Bypass Security Mechanisms](hardware-hacking/bypassing-security/)
    * Introduction to [Voltage Glitching](hardware-hacking/bypassing-security/voltage-glitching/)
  * How to [analyze Firmware](hardware-hacking/analyze-firmware.md)
* [Network Analysis](network-analysis/introduction.md)
  * How to analyze protocols: [Reverse Engineering ](network-analysis/protocols/application-layer/proprietary-protocols/parrot-anafi-drone-reverse-engineering.md)a drone
* [Radio Hacking](radio-hacking/introduction.md)
  * Tools ([RTL-SDR](radio-hacking/tools/rf-signal-analyzers/rtl-sdr.md),[ Flipper Zero](radio-hacking/tools/flipper-zero/))
  * Protocols ([RFID](radio-hacking/protocols/rfid.md), [NFC](radio-hacking/tools/flipper-zero/nfc.md)) and how to hack them

## How You Can Contribute

We strongly encourage anyone interested to contribute their knowledge and insights. By sharing your discoveries or improving existing content, you help build a valuable resource for everyone.

To contribute:

* Submit a pull request on our [GitHub repository](https://github.com/F3enter/HardBreak)
* Help us keep the content accurate—if you notice an error, please report it so we can correct it quickly! Reach out on [LinkedIn](https://www.linkedin.com/in/jonas-rosenberger-3276b1164/) or [Twitter](https://x.com/HardBreakWiki)

{% hint style="info" %}
Reference the original source or blog whenever you include content from another author.
{% endhint %}

Check out our [Contribution Guide](contribute/how-to-contribute.md) for a step-by-step tutorial to making your first pull request!

## Important Disclaimers

{% hint style="warning" %}
While this wiki is built with the best knowledge and intentions from our contributors, **it may contain errors**. We encourage users to double-check any advice or strategies before applying them in practice. If you spot an issue, please help us by reporting it or making an edit!
{% endhint %}

#### Educational Use Only

{% hint style="danger" %}
The strategies and advice shared on this site are for **educational and informational purposes only**. They should not be used for any unlawful or harmful activities. We do not endorse or encourage any illegal or unethical conduct. Use the information here responsibly and at your own risk.
{% endhint %}

## Get Started

<table data-view="cards"><thead><tr><th></th><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Introduction</strong></td><td>How to start</td><td></td><td></td><td><a href="introduction/how-to-start.md">how-to-start.md</a></td></tr><tr><td><strong>Basics</strong></td><td>Hardware Hacking Tools</td><td></td><td></td><td><a href="hardware-hacking/basics/tools/hardware-tools/">hardware-tools</a></td></tr><tr><td><strong>Hardware Hacking</strong></td><td>Extracting Firmware using UART</td><td></td><td></td><td><a href="hardware-hacking/interface-interaction/uart/extract-firmware-using-uart.md">extract-firmware-using-uart.md</a></td></tr><tr><td><strong>Reverse Engineering</strong></td><td>Hacking a drone</td><td></td><td></td><td><a href="network-analysis/protocols/application-layer/proprietary-protocols/parrot-anafi-drone-reverse-engineering.md">parrot-anafi-drone-reverse-engineering.md</a></td></tr></tbody></table>
