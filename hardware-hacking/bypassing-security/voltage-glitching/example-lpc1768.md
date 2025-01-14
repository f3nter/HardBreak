# Example: LPC1768

In this chapter I want to give you an example of how glitching attacks work in detail. Scenario: LPC1768 has a Code Read Protection (CRP) set, so that we can't access its JTAG interface.

## The Target: LPC1768

The NXP LPC1700 MCU family is built on an ARM Cortex M3 core, offering a balance of performance and power efficiency. NXP provides four security levels, including CRP0, which allows unrestricted access. The MCU supports UART and JTAG interfaces and includes a bootloader that operates via UART. To activate the bootloader, the Reset pin and P2.10 pin must be held low.

Synchronization with a connected machine is initiated by sending the “?” character to the MCU, which responds with “Synchronized/\r\n.” The user must then resend this response to receive “OK\r\n.” Next, the user sets the clock rate to 12 MHz by sending “12000\r\n,” to which the LPC responds with “OK\r\n.” After synchronization, the user can read 4 bytes from address 0 using the command “R 0 4\r\n,” which returns the data and confirms with “OK\r\n.” If access is denied due to insufficient rights, the MCU responds with the error code “19.”

Different Code Read Protection (CRP) levels on NXP LPC17xx chips (every other pattern will result in CRP0=full access):

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

## Thoughts and Strategy

Here are some key features and thought to keep in mind

* CRP Level Determination:
  * Is set during the bootup process of the bootloader.
  * The bootloader reads a value(CRP level) from a specific flash offset preset by the manufacturer.
* CRP Level Vulnerability:
  * Each non-specific value defaults to CRP Level 0.
  * Only a single bit flip can deactivate the CRP level, making it fragile.
* Security Bypass:
  * Voltage glitching could potentially bypass the CRP security mechanism.
  * <mark style="color:blue;">**Concept**</mark><mark style="color:blue;">: Implement a glitch tactic where none of the CRP values are interpreted correctly, defaulting the system to CRP0. This vulnerability could potentially allow unrestricted access to the device</mark>
  * But we are not sure when the CRP check is performed after reset, and what exact parameter the glitch should have (offset, width, voltage), so we need to bruteforce those

## Setup

<figure><img src="../../../.gitbook/assets/glitch aufbau.png" alt=""><figcaption><p>Glitch setup with FPGA</p></figcaption></figure>

* Setup for Glitching:
  * Connect GND, VCC, P2.10, and RESET pins with the voltage glitch FPGA.
  * Connect GND, RXD, and TXD with a serial to USB cable.
  * The FPGA powers the LPC and enables the bootloader while holding P2.10 and RESET low.
* Glitch Parameter Configuration:
  * Use a Python script which will brute force the glitch parameters (offset, voltage level and width of glitch)
* Step-by-step:
  1. target chip starts
  2. we will perform a glitch (varying offset, width and voltage of glitch)
  3. perform UART check if we can read data  “R 0 4 \r \n”
  4. if error code "19" is read, start with new parameters
  5. run until we can read data => then we have a successful glitch

According to Andrea Baccega if the Brown-Detection (which resets the chip, if the voltage is too low) is enabled, you can disable it [by connecting P2\[13\] of LPC1768 to GND upon boot.](https://github.com/vekexasia/lpc_voltage_glitch_test)

## Resources

[https://github.com/vekexasia/lpc\_voltage\_glitch\_test](https://github.com/vekexasia/lpc_voltage_glitch_test)

