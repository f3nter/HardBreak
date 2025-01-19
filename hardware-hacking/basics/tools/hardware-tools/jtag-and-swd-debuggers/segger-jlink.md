# Segger JLink

J-Link is a series of powerful JTAG and SWD debug probes developed by Segger. They are widely used for debugging and programming ARM microcontrollers and other embedded systems. The J-Link debuggers are known for their speed, reliability, and compatibility with a wide range of development tools and environments, making them a preferred choice among embedded developers and hardware pentesters.

## Features

* Multi-Interface Support
  * J-Link supports both JTAG and SWD protocols, allowing it to work with various microcontroller architectures.
* High-Speed Performance
  * It offers fast data transfer rates, enabling quicker debugging sessions and programming.
* Cross-Platform Compatibility
  * Works seamlessly with popular IDEs like Keil, IAR Embedded Workbench, and Eclipse.
* Extensive Support
  * Provides a comprehensive software package, including J-Link software and documentation, making it easier to get started.

## Cheat Sheet

```bash
# Connect to J-Link device
JLinkExe.exe

# Connect to a target device (select device from pop up window)
connect

# Halt the target CPU
halt

# Reset the target CPU
r  # or 'reset'

# Reset and halt the CPU
reset halt

# Read memory at a specified address
mem32 <address> <count>  # Reads 32-bit words from memory

#Read complete flash and save it
savebin <filename.bin> <start address> <size>

# Write memory to a specified address
w1 <address> <value>     # Write 1 byte
w2 <address> <value>     # Write 2 bytes
w4 <address> <value>     # Write 4 bytes

# Load a binary file into the target device memory
loadbin <file> <address>

# Dump memory to a binary file
savebin <file> <address> <size>
savebin flash_dump.bin 0x08000000 0x00040000 #example

# Set a breakpoint
setbp <address>

# Clear a breakpoint
clrbp <address>

# Step through instructions
step

# Continue execution
go

# Exit J-Link Commander
q  # or 'exit'
```

#### Example Commands to Dump a Flash Chip Using J-Link

To dump a flash chip using J-Link, you can use the J-Link Command Line Interface (CLI) or the J-Link GDB Server. Below is an example using the J-Link CLI, which is part of the J-Link software package:

1. Open the Command Prompt (or Terminal on macOS/Linux).
2. Navigate to the J-Link installation directory where the CLI tool is located, usually found under `C:\Program Files (x86)\SEGGER\JLink` on Windows.
3. Connect the J-Link Debugger to your target device and power it on.
4.  Run the J-Link Command Line Tool:

    ```bash
    JLink.exe
    ```

    <figure><img src="../../../../../.gitbook/assets/image (30).png" alt="" width="484"><figcaption></figcaption></figure>
5.  Connect to the Target Device: In the J-Link Command Line interface, use the following command:

    ```bash
    connect
    ```

    * Select the Device: Choose the specific device you are targeting (e.g., `STM32F4xx`).
    * Select Interface: Choose either `SWD` or `JTAG` based on your connection type.
    * Specify the Speed: Set the desired speed (default is usually fine).

    <figure><img src="../../../../../.gitbook/assets/aktive cJtag.png" alt=""><figcaption><p>Successful cJTAG connection</p></figcaption></figure>
6.  Dump the Flash Memory:&#x20;

    ```bash
    savebin <filename.bin> <start address> <size>
    ```

    * `<filename.bin>`: The name of the output file where the flash dump will be saved.
    * `<start address>`: The starting address of the flash memory you want to dump (e.g., `0x08000000` for STM32).
    * `<size>`: The number of bytes to dump (e.g., `0x00040000` for 256KB).

    Example:

    ```bash
    savebin flash_dump.bin 0x08000000 0x00040000
    ```
7.  Exit the J-Link Command Line Tool

    ```bash
    exit
    ```

#### Resources

* [J-Link Commander](https://kb.segger.com/J-Link_Commander)
