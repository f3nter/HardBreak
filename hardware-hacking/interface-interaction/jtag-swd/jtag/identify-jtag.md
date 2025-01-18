# Identify JTAG

### 1. **Reminder of the Basics of JTAG**

JTAG is typically implemented using the following standard signals, which we need to find:

* **TDI**: Test Data In
* **TDO**: Test Data Out
* **TCK**: Test Clock
* **TMS**: Test Mode Select
* **TRST**: Test Reset (optional)

### 2. **Preliminary Examination**

* **Inspect the PCB Layout**
  * Look for **pin headers** or **test points** with 4-10 pins in a row or dual row configuration.
  * Check for labeled pads or silkscreen markings such as **JTAG**, **TDI**, **TDO**, etc.
  * Examine components for known JTAG-compatible chips (e.g., ARM Cortex processors, FPGAs).
* **Consult the Datasheet**
  * Identify major ICs on the PCB and locate their datasheets online. Search for:
  * JTAG or boundary scan capabilities.
  * Pin numbers corresponding to JTAG signals.
* &#x20;**Look for Clues**
  * Use magnification to inspect nearby traces. JTAG pins often connect directly to the processor or debug interfaces.
  * Check for standardized pinouts like ARM’s 20-pin or 10-pin connectors.

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption><p>Potential JTAG interface</p></figcaption></figure>

### 3. **Test for Common JTAG Pinouts**

Here are a few common JTAG pinouts to reference:

<figure><img src="../../../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption><p>Common JTAG pinouts</p></figcaption></figure>

### 4. **Electrical Verification**

* **Check Pin Voltage Levels**
  * Using a multimeter, measure the voltage on suspected pins when the device is powered on:
    * **TDI, TDO, TMS, TCK**: Typically operate at 1.8V, 3.3V, or 5V.
    * **GND**: Should read 0V.
    * **Vcc**: Will match the system voltage (e.g., 3.3V or 5V).
* **Probe Continuity**
  * Use a multimeter in continuity mode to trace suspected pins:
    * Test connections between suspected pins and the processor’s JTAG pins (refer to the datasheet).
    * Identify Vcc and GND connections to nearby capacitors or power lines.

{% hint style="info" %}
Depending on the GND and VCC pins  we can limit the number of possible JTAG pinouts!
{% endhint %}

### 5. **Verification Using Test Tools**

**a) Use a JTAG Finder**

Tools like JTAGulator or Bus Pirate can assist in identifying JTAG signals by probing the pins automatically.

b) **Connect a Debugger**

1. Attach a known JTAG debugger (e.g., OpenOCD or Segger J-Link) to the suspected interface.
2. Use debugging software to scan for a JTAG chain.
3. Look for a valid response to confirm the JTAG interface.

### 6. **Analyze Signal Activity**

a) **Use an Oscilloscope or Logic Analyzer**

1. Monitor pin activity during device operation or reset.
2. Look for:
   * Clock signals on **TCK**.
   * Data transitions on **TDI**, **TDO**, or **TMS**.

b) **Identify Pull-Up Resistors**

Check if certain pins have pull-up resistors to Vcc, which is common for **TMS** or **TDI**.

## Resources

* [Hardware Hacking 101: Identifying and Verifying JTAG on a Device](https://riverloopsecurity.com/blog/2021/05/hw-101-jtag-part2/)
* [Technical Guide to JTAG](https://www.xjtag.com/about-jtag/jtag-a-technical-overview/)
* [Hardware Hacking Experiments: Extracting Firmware from Embedded Device](https://github.com/koutto/hardware-hacking/blob/master/Hardware-Hacking-Experiments-Jeremy-Brun-Nouvion-2020.pdf)
