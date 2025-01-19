# JTAG

## **Theory**

JTAG (Joint Test Action Group) is a standard interface used for testing, debugging, and programming embedded systems, especially microcontrollers and FPGAs. JTAG is often used during development to diagnose hardware issues or to program devices in-system. It allows direct access to a device’s memory, registers, and other critical functions. For pentesters, exploiting JTAG can provide deep insights into a device’s internals, enabling you to extract firmware, bypass security mechanisms, or alter device behavior. (Technical guide at the end of the page)

## **Requirements:**

1. Hardware
   * JTAG Adapter (e.g., Bus Pirate, Segger J-Link, FTDI-based adapters, or OpenOCD-compatible adapters)
   * Jumper wires to connect the JTAG adapter to the target device
   * Multimeter to check voltages and identify JTAG pins
   * Soldering kit (if JTAG pins are not exposed)
2. Software (choose one, which supports your debugger)
   * OpenOCD (Open On-Chip Debugger) for JTAG interaction
   * UrJTAG (open-source JTAG tools)
   * GDB (GNU Debugger) for debugging over JTAG
   * J-Link software (for Segger J-Link adapters)
   * Binwalk (for firmware analysis after extraction)

## **Usage**

1.  Identifying JTAG Pins:

    * JTAG typically uses multiple pins, including:
      * TDI (Test Data In): Data input to the device.
      * TDO (Test Data Out): Data output from the device.
      * TCK (Test Clock): Clock signal for synchronization.
      * TMS (Test Mode Select): Mode selection signal.
      * TRST (Test Reset, optional): Resets the JTAG state machine.
    * Use a multimeter to check voltage levels on the JTAG header (typically 3.3V or 5V).

    Command Example (OpenOCD for Pin Identification):

    ```bash
    openocd -f interface/ftdi.cfg -f target/your_target.cfg -c "init; scan_chain; shutdown"
    ```

    This command initializes the connection to the JTAG chain and identifies connected devices.
2.  Dumping Firmware via JTAG:

    * Once the target device is discovered, JTAG can be used to dump the firmware from the device’s memory. This is a crucial step in analyzing the system for vulnerabilities, backdoors, or sensitive information.

    Command Example (Dumping Memory via OpenOCD):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "init; dump_image firmware.bin 0x08000000 0x10000; shutdown"
    ```

    This dumps the firmware (size 0x10000 bytes) from memory address `0x08000000` to a file named `firmware.bin`. (check the datasheet of your target MCU where the firmware is stored+how big it is and change the command accordingly)
3.  Modifying Firmware:

    * JTAG allows you to write directly to the device’s memory, including reprogramming the flash with modified firmware. This can be used to inject backdoors, modify settings, or tamper with system functions.

    Command Example (Flashing Firmware via OpenOCD):

    ```bash
    openocd -f interface/jlink.cfg -f target/stm32f4x.cfg -c "program modified_firmware.bin 0x08000000 verify reset exit"
    ```

    This writes the `modified_firmware.bin` file to the target device and verifies the changes.
4.  Debugging and Code Execution:

    * JTAG allows setting breakpoints and stepping through code, making it a powerful tool for debugging. You can halt execution, inspect memory, and control the flow of execution to analyze or bypass security mechanisms.

    Command Example (Attaching GDB to a JTAG Device):

    ```bash
    gdb-multiarch firmware.elf
    (gdb) target remote :3333
    (gdb) monitor reset halt
    (gdb) break main
    (gdb) continue
    ```

    This attaches GDB to the target device and sets a breakpoint at the `main` function.

## Technical Guide (not needed for Beginners)

#### Boundary Scan Overview

**Boundary scan** enables testing and debugging of devices by controlling and monitoring pin values without requiring physical access. This is achieved through the **Boundary Scan Register (BSR)**, a series of boundary scan cells that intercept signals between a device’s core logic and its pins. In normal operation, these cells are transparent, but in test mode, they allow setting or reading of values from pins or internal logic.

#### JTAG Interface Signals (TAP)

The **Test Access Port (TAP)** uses the following signals for boundary scan operations:

* **TMS (Test Mode Select)**: Determines the next state of the TAP controller.
* **TDI (Test Data In)**: Inputs data into the device's test or programming logic.
* **TDO (Test Data Out)**: Outputs data from the device's test or programming logic.
* **TRST (Test Reset)** (optional): Resets the TAP controller.
* **TCK (Test Clock)**: Synchronizes the TAP controller and state machine operations.

#### Registers in Boundary Scan

Boundary scan uses two main types of registers:

1. **Instruction Register**: Holds the current instruction, determining which data register to operate on.
2. **Data Registers**:
   * **BSR (Boundary Scan Register)**: Transfers data to and from device pins for testing.
   * **BYPASS Register**: A single-bit register for quick data passthrough, minimizing overhead during multi-device testing.
   * **IDCODES Register**: Contains the device's ID and revision number, linking it to its Boundary Scan Description Language (BSDL) file.

#### TAP Controller

The TAP controller is a state machine controlled by the **TMS signal**, which transitions through states based on the IEEE 1149.1 JTAG standard. These states allow for:

* Shifting data into or out of the **Instruction Register** or **Data Registers** (e.g., BSR, IDCODES, BYPASS).
* Updating register values to interact with device pins or core logic.

#### Common JTAG Instructions

1. **BYPASS**: Routes data directly from **TDI** to **TDO**, skipping internal logic for quick testing of other devices in the JTAG chain.
2. **EXTEST**: Uses the BSR to control and test pin states by shifting in new values and updating pins.
3. **SAMPLE/PRELOAD**: Samples functional data or preloads test data into the BSR while the device operates normally.
4. **IDCODE**: Accesses the IDCODES register to read the device’s unique ID.
5. **INTEST**: Operates on the core-logic signals of the device, rather than its pin states.

## Resources

*[A Hacker’s Guide To JTAG](https://hackaday.com/2020/04/08/a-hackers-guide-to-jtag/)
*[Hardware Hacking 101: Introduction to JTAG](https://riverloopsecurity.com/blog/2021/05/hw-101-jtag/)
*[Bus Blaster urJTAG guide](http://dangerousprototypes.com/docs/Bus\_Blaster\_urJTAG\_guide)
*[Technical Guide to JTAG](https://www.xjtag.com/about-jtag/jtag-a-technical-overview/)
