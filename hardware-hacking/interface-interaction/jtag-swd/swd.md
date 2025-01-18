# SWD

## **Theory**

SWD (Serial Wire Debug) is a 2-wire protocol used primarily for debugging ARM-based microcontrollers. It provides a lightweight alternative to JTAG (which uses multiple wires) while offering similar debugging capabilities. SWD allows direct access to the core of the microcontroller, enabling read/write access to memory, setting breakpoints, and controlling program execution.

Pentesters often use SWD to reverse engineer firmware, modify device behavior, extract sensitive data, or bypass security mechanisms during hardware assessments.

## **Requirements**

1. Hardware
   * SWD Adapter (e.g., ST-Link, J-Link, or DAPLink)
   * Jumper wires for connecting the SWD interface to the target device
   * Multimeter (for voltage checks and pin identification)
   * Soldering kit (if the SWD interface isn't exposed)
2. Software
   * OpenOCD (Open On-Chip Debugger) for interacting with SWD
   * ST-Link Utility or J-Link software for specific adapters
   * GDB (GNU Debugger) for debugging over SWD
3. Best Pratices
   * Always verify the correct pinout and connection before interfacing with SWD, as incorrect wiring can damage the microcontroller.
   * Ensure your SWD adapter supports the voltage level of the target device (usually 3.3V or 5V)
   * Before modifying or erasing any memory, make sure to dump the existing firmware in case recovery is needed later.

## **Common Attacks**

1.  Identifying SWD Pins

    * SWD consists of two main pins:
      * SWDIO (Serial Wire Debug Input/Output): Carries data between the debugger and the microcontroller.
      * SWCLK (Serial Wire Clock): Provides the clock signal for synchronization.
    * Use a multimeter to check continuity and voltage levels to identify SWDIO, SWCLK, and GND. Typically, SWD pins are part of a header on the device or exposed as test pads.

    Command Example (OpenOCD Pin Setup):

    ```bash
    openocd -f interface/stlink.cfg -f target/stm32f1x.cfg
    ```

    This command sets up OpenOCD to connect via an ST-Link adapter and target an STM32 microcontroller.
2.  Reading and Dumping Firmware

    * Once connected, you can dump the contents of the device’s memory (including firmware) using SWD. This can give you access to sensitive information or code that you can reverse engineer.

    Command Example (Dumping Firmware using OpenOCD):

    ```bash
    openocd -f interface/stlink.cfg -f target/stm32f1x.cfg -c "init; dump_image firmware.bin 0x08000000 0x10000; shutdown"
    ```

    This dumps the firmware from memory address `0x08000000` to a file named `firmware.bin`.
3.  Modifying or Restoring Firmware&#x20;

    * You can also modify the device’s firmware or configuration in memory. This is useful for injecting backdoors, altering security settings, or unlocking device features.

    Command Example (Writing to Flash using OpenOCD):

    ```bash
    openocd -f interface/stlink.cfg -f target/stm32f1x.cfg -c "program new_firmware.bin 0x08000000 verify reset exit"
    ```

    This flashes `new_firmware.bin` to the microcontroller and verifies it.
4.  Debugging and Breakpoints

    * SWD allows setting breakpoints and stepping through code for reverse engineering or bypassing security functions in real time.

    Command Example (Attaching GDB to a Target):

    ```bash
    gdb-multiarch firmware.elf
    (gdb) target remote :3333
    (gdb) monitor reset init
    (gdb) break main
    (gdb) continue
    ```

    This attaches GDB to the target device and sets a breakpoint at the `main` function.

## Resources

* [Unveiling Vulnerabilities: Exploring SWD Attack Surface in Hardware](https://redfoxsec.com/blog/unveiling-vulnerabilities-exploring-swd-attack-surface-in-hardware/)
* [Find SWD Points Quickly, No Extra Hardware Needed](https://hackaday.com/2023/01/31/find-swd-points-quickly-no-extra-hardware-needed/)
