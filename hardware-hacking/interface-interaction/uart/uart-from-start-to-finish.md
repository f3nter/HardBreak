# Identify UART

This page should will teach you how to identify an [UART](./) interface. If you already confirmed the found debug connector is using UART you may continue with[ Connect to UART](connect-to-uart.md).

To interact with a UART interface, you would need:

* A multimeter
* an USB to UART TTL adapter
* jumper cables
* and in some cases: a soldering station

After opening the device follow the following steps to identify UART.

## **Get an overview**

1. Checkout which chips are used
   1. Google the datasheet of each chip you find (model should be printed on top of the chip)
   2.  It can be useful to take a picture of the PCB and label everything you can identify

       <figure><img src="../../../.gitbook/assets/komplett-beschriftet (1).png" alt="" width="375"><figcaption><p>Example layout of an PCB</p></figcaption></figure>
2.  Check for connector or test pads

    1. For UART we need pins: TX,RX,GND often manufacturers also put a VCC pin next to power the device. So we are looking for 4 pads or pins on the PCB board, like here:

    <figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt="" width="188"><figcaption><p>Potential UART pins</p></figcaption></figure>

    1. Even better if we find actual pins, where we can connect jumper cables to:

    <figure><img src="../../../.gitbook/assets/image (31).png" alt="" width="172"><figcaption><p>Uart pins exposed</p></figcaption></figure>

## **Test potential UART pins**

To verify if the identified pins are UART, we can use a multimeter. The simplest approach is to test for continuity between the suspected pins and the known UART pins on the MCU, as indicated in its datasheet. However, if the MCU has a BGA layout with pins beneath the chip, this method won't work. In such cases, measuring the voltage of the suspected pins can help make an educated guess to identify the correct ones.

{% tabs %}
{% tab title="Continuity test" %}
The first step is to put your multimeter in continuity mode (often a "sound" symbol). This mode will check if there is a direct link between two points on the PCB

<figure><img src="../../../.gitbook/assets/image (6).png" alt="" width="338"><figcaption><p>Multimeter in continuity mode</p></figcaption></figure>

Next we need identify a reference point to check against. Luckily manufacturers provide us often with datasheets of their MCUs, which include the pinout of the chip. So google your chip and find the TXD, RXD pins in the datasheet, like here:

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt="" width="282"><figcaption><p>Example UART pins</p></figcaption></figure>

Now we can start our continuity test:

* Put one probe on the connector pad you want to test
* The other one should be on the exact pin on the chip (RX or TX).
* It should look like this:

<figure><img src="../../../.gitbook/assets/image (5).png" alt="" width="287"><figcaption><p>How to probe</p></figcaption></figure>

If you hear a BEEP, then there is a direct link between the pin and the pad you checked. You need to find the GND (ground), TX (transmit) and RX(receive) pins to communicate with UART.
{% endtab %}

{% tab title="Voltage test" %}
Try this technique when booting up the device, as the device will print out a lot of stuff over UART and we can therefore identify RX and TX better.

\
If you can't use the microchips pins as reference (for example if it's a BGA chip or if there is no datasheet) you can check the voltage of the pins:

* High constant (around 3.3V or 5V are the most common) indicates VCC
* If the voltage fluctuates this may indicate data transmission and therefore the TX pin of the chip (reminder: has to be connected to RX on your UART adapter NOT TX)
* Zero voltage indicates GND
* Depending on the UART configuration the RX pin is either idle high or idle low, so it is not so easy to differentiale it from GND or VCC

Here a summary:

| Voltage Range         | Signal |
| --------------------- | ------ |
| 3.3V-5V Vcc           | Vcc    |
| 1.7-2.5V (fluctuates) | Tx     |
| 0-0.004V OR 3.3-5V    | Rx     |
| 0V                    | GND    |
{% endtab %}

{% tab title="Restance check" %}
Another method is to check the resistance of each test pad against GND.

Here would be the expected values, but it also is depending on the configuration:

| Resistance                          | Signal |
| ----------------------------------- | ------ |
| ∞                                   | Vcc    |
| \~80kΩ                              | Tx     |
| \~12kΩ                              | Rx     |
| 0Ω (should beep in continuity mode) | GND    |
{% endtab %}
{% endtabs %}

## Next Step

If you could identify all the needed pins, you may now [Connect to UART](connect-to-uart.md).

## Resources

\*[Hardware Hacking: Finding UART Pinouts on PCBs](https://www.secureideas.com/blog/hardware-hacking-finding-uart-pinouts-on-pcbs)

\*[Hardware Hacking Experiments: Extracting Firmware from Embedded Device](https://github.com/koutto/hardware-hacking/blob/master/Hardware-Hacking-Experiments-Jeremy-Brun-Nouvion-2020.pdf) \*[Decoding the Mystery: Identifying Unlabelled UART Pins](https://redfoxsec.com/blog/decoding-the-mystery-identifying-unlabelled-uart-pins/)
