# Extract Firmware using JTAG/SWD

If you found an active JTAG/SWD interface on a PCB it can be used to extract the firmware in some cases.

### Requirements

#### Hardware

1. Target Device
2. JTAG/SWD Debugger ( like ST-Link, J-Link, or Bus Pirate.
3. JTAG/SWD Header/Pinout (TCK, TMS, TDI, TDO for JTAG or SWDIO, SWCLK for SWD).
4. Jumper Wires (to connect the debugger to the target device)
5. Power Source

#### Software

1. Debugger-Tools: Open On-Chip Debugger (OpenOCD) or JLINK-Commander software for communicating with the JTAG/SWD interface.
2. Drivers: Drivers for your specific debugger (e.g., ST-Link or J-Link drivers).

## **Steps to Extract Firmware Over JTAG/SWD**

#### 1. **Identify JTAG/SWD Pins**

* Locate the JTAG or SWD pins on the target device. These are often labeled as follows:
  * JTAG Pins:
    * TCK (Test Clock)
    * TMS (Test Mode Select)
    * TDI (Test Data In)
    * TDO (Test Data Out)
    * GND (Ground)
  * SWD Pins:
    * SWDIO (Serial Wire Data Input/Output)
    * SWCLK (Serial Wire Clock)
    * GND (Ground)
* Consult the device datasheet or use tools like a multimeter or datasheets to map out the connections.

#### 2. **Connect the Debugger**

* Use jumper wires to connect the JTAG/SWD pins on the target device to the corresponding pins on the debugger:
  * For JTAG: Connect TCK, TMS, TDI, TDO, and GND. (sometimes also RESET is needed)
  * For SWD: Connect SWDIO, SWCLK, and GND.
* Make sure the connections are secure to avoid communication failures.

#### 3. **Set Up Software and Dump firmware**

{% tabs %}
{% tab title="OpenOCD" %}
1. Install **OpenOCD** to manage communication between your debugger and the target device.
2. **GDB**: Install GNU Debugger for low-level device control.

#### **Configure OpenOCD**

* OpenOCD needs to be configured with the appropriate settings for your device. You can use pre-existing configuration files or create your own. For example:
*   Create a configuration file (`my_device.cfg`) that defines the target and interface:

    ```cfg
    interface jlink
    transport select jtag
    source [find target/stm32f1x.cfg]  ; for an STM32 device, adapt for others
    ```
* Then, launch OpenOCD with:
* ```bash
  openocd -f interface/jlink.cfg -f target/my_device.cfg
  ```

If the connection is correct we should see an output like this:

```
Open On-Chip Debugger 0.11.0 (2024-10-07) 
Licensed under GNU GPL v2
For bug reports, read
	http://openocd.org/doc/doxygen/bugs.html
Info : J-Link V10 compiled Aug  3 2024 15:23:43
Info : Hardware version: 10.10
Info : VTarget = 3.300 V
Info : clock speed 1000 kHz
Info : JTAG tap: stm32f429x.cpu tap/device found: 0x2ba01477 (mfg: 0x23b, part: 0xba01, ver: 0x2)
Info : stm32f429x.cpu: hardware has 8 breakpoints, 4 watchpoints
Info : starting gdb server for stm32f429x.cpu on 3333
Info : Listening on port 4444 for telnet connections
Info : Listening on port 3333 for gdb connections
```

We can see that we have two options to interact with OpenOCD: **telnet** and **gdb**

**Telnet:**&#x20;

1. **Connect to OpenOCD via Telnet**:

Open a separate terminal and connect to the OpenOCD server:

```bash
telnet localhost 4444
```

2. **Successful connection output**:

Once connected, you should see something like this:

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Open On-Chip Debugger
```

3. **Commands you can use via Telnet**:

Here are a few example commands you might use via Telnet:

```
> reset halt                  # Reset and halt the target
> flash write_image erase firmware.bin 0x08000000  # Write firmware to flash memory
> mdw 0x08000000              # Read a memory word (32-bit) at the specified address
> mww 0x20000000 0x12345678   # Write a memory word (32-bit) to the specified address
> step                        # Step through the target's instructions
> resume                      # Continue execution
```

**GDB:**

<pre class="language-bash"><code class="lang-bash"># Launch GDB
arm-none-eabi-gdb

# Inside GDB, connect to OpenOCD via localhost on port 3333
(gdb) target remote localhost:3333

# Perform a reset and halt the target
(gdb) monitor reset halt

# Dump the firmware of the target
(gdb) dump binary memory &#x3C;filename> &#x3C;start-address> &#x3C;end-address>
# example /Adjust the memory address range based on your target device’s memory map):
<strong>(gdb) dump binary memory firmware.bin 0x08000000 0x080FFFFF
</strong>
# Continue execution
(gdb) continue
</code></pre>
{% endtab %}

{% tab title="Jlink.exe" %}
#### Commands to Dump Firmware Using J-Link Commander

1.  **Start J-Link Commander**: Run the `JLinkExe` command to launch J-Link Commander.

    ```bash
    JLinkExe
    ```
2.  **Connect to the Target**: You will need to specify the target device and the connection interface. For example, for an STM32F4 target connected via JTAG, you might see the following prompt:

    ```yaml
    SEGGER J-Link Commander V6.88b (Compiled Jul 22 2024 16:21:34)
    DLL version V6.88b, compiled Jul 22 2024 16:21:06

    Connecting to J-Link via USB...O.K.
    Firmware: J-Link ARM V10 compiled Jul  3 2024 14:22:47
    Hardware: V10.10
    S/N: 123456789
    License(s): RDI, FlashBP, GDB
    VTref=3.300V
    ```

    **Enter the target details**:

    ```
    Device> STM32F429ZI  # Replace with your target device
    ```

    **Interface selection**:

    ```
    TIF> JTAG  # Or SWD, depending on your setup
    ```
3.  **Halt the Target**: To ensure a consistent firmware dump, halt the CPU:

    ```bash
    halt
    ```

    **Expected output**:

    ```
    PC = 0x08000100, CycleCnt = 0x00000000
    R0 = 0x20000000, R1 = 0x08001000, R2 = 0x20002000, R3 = 0x00000000
    R4 = 0x00000000, R5 = 0x00000000, R6 = 0x00000000, R7 = 0x00000000
    R8 = 0x00000000, R9 = 0x00000000, R10= 0x00000000, R11= 0x00000000
    R12= 0x00000000, SP (R13)= 0x20002000, LR (R14)= 0x0800055F, PC = 0x08000100
    CPSR = 0x60000010
    ```
4.  **Read Memory and Dump to a File**: Use the `savebin` command to dump the firmware (Adjust the Offset and size depending on your targets memory map).

    ```bash
    savebin firmware_dump.bin 0x08000000 0x10000
    ```

    * `firmware_dump.bin`: The name of the binary file where the memory content will be saved.
    * `0x08000000`: Start address of the firmware (for most STM32 devices, this is the start of flash memory).
    * `0x10000`: The size of the memory region to dump (in this case, 64KB).

#### Full Example Session

```bash
$ JLinkExe
SEGGER J-Link Commander V6.88b (Compiled Jul 22 2024 16:21:34)
DLL version V6.88b, compiled Jul 22 2024 16:21:06

Connecting to J-Link via USB...O.K.
Firmware: J-Link ARM V10 compiled Jul  3 2024 14:22:47
Hardware: V10.10
S/N: 123456789
License(s): RDI, FlashBP, GDB
VTref=3.300V

Device> STM32F429ZI
TIF> JTAG
Speed> 1000  # Set speed to 1 MHz

JTAG speed set to 1000 kHz
Device "STM32F429ZI" selected.


J-Link> halt
PC = 0x08000100, CycleCnt = 0x00000000
R0 = 0x20000000, R1 = 0x08001000, R2 = 0x20002000, R3 = 0x00000000
R4 = 0x00000000, R5 = 0x00000000, R6 = 0x00000000, R7 = 0x00000000
R8 = 0x00000000, R9 = 0x00000000, R10= 0x00000000, R11= 0x00000000
R12= 0x00000000, SP (R13)= 0x20002000, LR (R14)= 0x0800055F, PC = 0x08000100
CPSR = 0x60000010

J-Link> savebin firmware_dump.bin 0x08000000 0x10000
Writing 65536 bytes to file firmware_dump.bin
O.K.
```
{% endtab %}
{% endtabs %}

### After dumping the firmware

\=> Jump to the [Analyze Firmware](../../analyze-firmware.md) section

## Resources

* [Extracting firmware from devices using JTAG](https://sergioprado.blog/2020-02-20-extracting-firmware-from-devices-using-jtag/)
* [Hardware Debugging for Reverse Engineers Part 2: JTAG, SSDs and Firmware Extraction](https://wrongbaud.github.io/posts/jtag-hdd/)
