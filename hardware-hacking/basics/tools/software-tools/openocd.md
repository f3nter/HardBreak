# OpenOCD

## **Theory**

OpenOCD (Open On-Chip Debugger) is an open-source debugging tool designed primarily for embedded systems. It is widely used by hardware developers and penetration testers alike to communicate with and control the internals of microcontrollers (MCUs) and System-on-Chips (SoCs). It provides debugging, in-system programming, and boundary-scan testing functionalities. OpenOCD connects to hardware using various communication interfaces such as JTAG (Joint Test Action Group), SWD (Serial Wire Debug), or similar protocols, which are typically used for debugging and flashing firmware on microcontrollers.

With OpenOCD, a user can interact with a target device at a low level, controlling registers, memory, and other essential hardware features. This can be useful in hardware hacking or penetration testing environments, where attackers are trying to reverse engineer or modify embedded systems to find vulnerabilities or access sensitive information.

Commonly, OpenOCD is paired with GDB (GNU Debugger) to provide a rich environment for debugging embedded applications. The debugger is capable of setting breakpoints, examining memory, and stepping through code execution, enabling precise control over what is happening on the device.

## **Cheat Sheet**

```bash
# Install OpenOCD on Linux
sudo apt-get install openocd

# Start OpenOCD with JLink debugger and STM32 target configuration
openocd -f interface/jlink.cfg -f stm32h7x.cfg

# Connect to OpenOCD via telnet
telnet 127.0.0.1 4444

#Connect to OpenOCD via gdb
gdb
(gdb) target extended-remote localhost:3333
(gdb) monitor reset halt
(gdb) load
(gdb) continue

# Halt the CPU
halt

# Reset and initialize the CPU
reset init

# Get flash memory information
halt; flash info 0

# Dump the flash memory to a file
halt; dump_image flashdump.bin 0x00000000 0xF90600
```

## **Usage**

An example of using OpenOCD is dumping the firmware of a microcontroller using a JTAG interface:

* Connect a JTAG programmer to the target device
  * Ensure proper pin alignment for TCK (Test Clock), TMS (Test Mode Select), TDI (Test Data In), TDO (Test Data Out), and GND
* Install OpenOCD on your system
  *   On a Linux system, use the following command to install it:

      ```bash
      sudo apt-get install openocd
      ```
* Create or download a configuration file for your target MCU or SoC
  * This file contains the specific instructions to communicate with the target device
*   Start OpenOCD with the configuration file (-f) for the interface you are using and the taregt

    *   Example command for Jlink Debugger and a STM32 taregt:

        ```bash
        openocd -f interface/jlink.cfg -f stm32h7x.cfg
        ```

        If everything is correct you should see output like this:

    ```bash
    Open On-Chip Debugger 0.11.0+dev-00035-g8d6f7c922-dirty (2021-03-16-19:11)
    Licensed under GNU GPL v2
    For bug reports, read
      http://openocd.org/doc/doxygen/bugs.html
    Info : auto-selecting first available session transport "jtag". To override use 'transport select <transport>'.
    adapter speed: 15000 kHz

    Info : Listening on port 6666 for tcl connections
    Info : Listening on port 4444 for telnet connections
    Info : J-Link V9 compiled Feb  2 2021 16:34:10
    Info : Hardware version: 9.30
    Info : VTarget = 2.609 V
    Info : clock speed 15000 kHz
    Info : JTAG tap: stm32h7x.cpu tap/device found: 0x6ba00477 (mfg: 0x23b (ARM Ltd.), part: 0xba00, ver: 0x6)
    Info : starting gdb server for ath79.cpu on 3333
    Info : Listening on port 3333 for gdb connections
    ```
* Open another terminal and connect with GDB to control the debugging session
  *   Example command to connect GDB to OpenOCD:

      ```
      gdb extended-remote :3333
      ```
  * Use GDB commands to control the microcontroller
    *   Set a breakpoint:

        ```kotlin
        break main
        ```
* To dump memory or read registers etc. we can use the telnet port
* Example commands:
  * ```bash
    telnet 127.0.0.1 4444   #connect to telnet
    halt                    #we can halt the cpu
    reset init              #we can also reset and initialize it again
    halt; flash info 0      #get flash information

    # to dump the flash we use: dump_image <filename> <address> <size>
    halt; dump_image flashdump.bin 0x00000000 0xF90600 
    ```

The dumped firmware can then be [analyzed](../../../analyze-firmware.md).

## Resources

* [Hardware Hacking 101: Communicating with JTAG via OpenOCD](https://riverloopsecurity.com/blog/2021/07/hw-101-jtag-part3/)
* [Open On-Chip Debugger: OpenOCD User’s Guide (PDF)](https://openocd.org/doc/pdf/openocd.pdf)
