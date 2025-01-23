# Connect to UART

#### At this point you should have:

* Understand what UART does (if not check: [UART](./))
* Identified UART pins (if not check:[ Identify UART](uart-from-start-to-finish.md))

## Connect to UART

You need to find the GND (ground), TX (transmit) and RX(receive) pins to send and receive data with UART (RX pin is not required to just read data).

When you connect the UART-USB adapter with the UART interface on the board, you have to connect RX and TX together like this:

<figure><img src="../../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Connect RX to TX and TX to RX</p></figcaption></figure>

There are different ways to connect to identified test pads:

{% tabs %}
{% tab title="Pins/Holes" %}
If you are lucky, you find header pins where you can connect jumper cables to it. This is the easiest way to connect your UART-to-TTL USB adapter to an UART interface.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Header pins exposed, connect jumper cables here<br><br></p></figcaption></figure>

If your device has holes in the pcb for the UART connection, you can attempt to put jumper cables through it and tilt them, so they have a solid contact point:

<figure><img src="../../../.gitbook/assets/IMG_8347.JPG" alt="" width="375"><figcaption><p>Put the male pins through the connector holes<br></p></figcaption></figure>
{% endtab %}

{% tab title="Clamps" %}
If you own clamps or grabbers, you can use them to hook them up to the UART connector. These clamps have small hooks which you can hookup to the connector. This is not very usable if you only have flat connector pads.

<figure><img src="../../../.gitbook/assets/IMG_8349.JPG" alt="" width="375"><figcaption><p>Clamp with Hook<br></p></figcaption></figure>

Here an example when the clamps are attached:

<figure><img src="../../../.gitbook/assets/IMG_8350.JPG" alt="" width="563"><figcaption><p>Clamps attached</p></figcaption></figure>
{% endtab %}

{% tab title="Soldering" %}
Another option is to solder cables to the connector you found. This is especially useful if you only find flat pads to connect to.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="246"><figcaption><p>2 cables soldered to UART</p></figcaption></figure>
{% endtab %}

{% tab title="Probes" %}
Next, you can also connect your adapter to the UART interface using probes like the professional [PCBite](https://sensepeek.com/) or self-printed versions like this one:

<figure><img src="../../../.gitbook/assets/IMG_0561.jpeg" alt="" width="375"><figcaption><p>Connect the needle pins to the UART interface</p></figcaption></figure>
{% endtab %}
{% endtabs %}

## Interact with UART

On your PC use the following command to communicate over UART (you may have to adjust the baud rate)

{% tabs %}
{% tab title="Linux" %}
<pre class="language-bash"><code class="lang-bash"><strong>sudo minicom -D /dev/ttyUSB0 -b 115200
</strong>sudo picocom -b 115200 -r -l /dev/ttyUSB0
</code></pre>

Change the 115200 with the baud rate of your device (how to identify: see below)
{% endtab %}

{% tab title="Windows" %}
**Using PuTTY (Windows)**:

* Select “Serial” and enter the COM port (e.g., COM3) and baud rate (115200).
{% endtab %}
{% endtabs %}

5. If you see readable data: You done it correctly!

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Bootlog</p></figcaption></figure>

6. **If you see unreadable data then you probably have the wrong baud rate. Example**

<figure><img src="../../../.gitbook/assets/image (53).png" alt=""><figcaption><p>Wrong baud rate produces unreadable data</p></figcaption></figure>

### **Identifying the correct baud rate**

* Quick win: Try to guess the baud rate, the most common ones are:
  * 9600, 38400, 19200, 57600, 115200 (which is probably the most common of all)
* [Baudrate.py](https://github.com/sickcodes/python3-baudrate) is a script, which tests automatically for different baud rates
*   You can also try to manually identify the correct baud rate using a [logic analyzer](../../basics/tools/hardware-tools/logic-analyzer/)

    * When hovering your capture with the mouse in the Saleae Logic Software you can see the the width is equal to 111.111kHZ which is very close to 115200, so we should choose this baud rate

    <figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Use logic analyzer to get correct baud rate</p></figcaption></figure>

**Congrats!** You found your first serial connection! Check out the UART chapter on how to use this to dump the firmware from the device.
