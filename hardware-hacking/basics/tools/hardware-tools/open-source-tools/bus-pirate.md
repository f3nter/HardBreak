# Bus Pirate

## Theory

The Bus Pirate is an open-source hardware tool designed for interfacing with and debugging various communication protocols, including SPI, I2C, UART, JTAG and more. It acts as a universal bus interface, allowing developers and hardware pentesters to communicate with and analyze electronic devices. Its versatility and ease of use make it a popular choice for hobbyists, engineers, and security researchers.

<figure><img src="../../../../../.gitbook/assets/image (27).png" alt=""><figcaption><p>Bus Pirate</p></figcaption></figure>

Here is the pinout for the different modes:

| **Mode**   | **MOSI** | **CLK** | **MISO** | CS  |
| ---------- | -------- | ------- | -------- | --- |
| **1-Wire** | DATA     |         |          |     |
| **UART**   | TX       |         | RX       |     |
| **I2C**    | SDA      | SCL     |          |     |
| **SPI**    | MOSI     | CLOCK   | MISO     | CS  |
| **JTAG**   | TDI      | TCK     | TDO      | TMS |

**Key Features**

* Multi-Protocol Support:&#x20;
  * Supports a wide range of protocols, including SPI, I2C, UART, 1-Wire, and more.
* Command-Line:&#x20;
  * Operates via a simple command-line interface, allowing for easy interaction and experimentation.
* Open-Source:&#x20;
  * The hardware and firmware are open-source, enabling customization and community contributions.
* Compact Size:&#x20;
  * Portable and easy to integrate into various projects.

## Cheat Sheet

```bash
# Read the flash chip using Bus Pirate with flashrom
flashrom -p buspirate_spi:dev=/dev/device,spispeed=frequency -r out.file

# Example command with specific device and speed
flashrom -p buspirate_spi:dev=/dev/ttyUSB0,spispeed=1M -r firmware.bin

# Connect to bus pirate directly
 minicom -b 115200 -8 -D /dev/ttyUSB0

# Set the Bus Pirate to SPI mode
HiZ> m
5  # Choose SPI mode

# Set SPI speed (e.g., 1 MHz)
b 1000

# Read data from the flash chip
r 

# Exit Bus Pirate session
q
```

## Usage

#### Example Setup Flashrom and Bus Pirate

Here we just need to run one command and [flashrom](https://www.flashrom.org/supported\_hw/supported\_prog/buspirate.html) will try to detect the flash chip. With -r we can read out the flash.

```bash
 flashrom -p buspirate_spi:dev=/dev/device,spispeed=frequency -r out.file
 
 #Example
 flashrom -p buspirate_spi:dev=/dev/ttyUSB0,spispeed=1M -r firmware.bin
```

#### Example Setup of native Bus Pirate

To dump a flash chip using the Bus Pirate, you'll typically interface it with the SPI protocol. Here’s a step-by-step guide to doing this:

1. Connect the Bus Pirate:
   * Connect the Bus Pirate to your computer via USB.
   * Connect the Bus Pirate to the target flash chip using the appropriate wiring (MOSI, MISO, SCK, CS, etc.). Ensure that the connections match the pinout of the flash chip.
2. Install the Bus Pirate Firmware (if not already installed):
   * Ensure you have the latest firmware on your Bus Pirate. You can check this on the [Bus Pirate website](https://buspirate.com/).
3. Open a Terminal:
   * Open a terminal emulator (like PuTTY, Tera Term, or a terminal on Linux) to communicate with the Bus Pirate.
4.  Enter Bus Pirate Mode:

    * Type the following command to enter the Bus Pirate interactive mode:

    ```plaintext
    /dev/ttyUSB0  (or the appropriate port)
    ```
5.  Set the Bus Pirate to SPI Mode:

    * Use the following command to set the Bus Pirate to SPI mode:

    ```plaintext
    HiZ> m
    1. HiZ
    2. 1-WIRE
    3. UART
    4. I2C
    5. SPI
    6. 2WIRE
    7. 3WIRE
    8. KEYB
    9. LCD
    x. exit(without change)
    ```

    * Choose (5) SPI mode by typing the corresponding number.
6.  Set the Speed:

    * Set the SPI speed (for example, 1 MHz):

    ```plaintext
    b 1000  (for 1 MHz)
    ```
7. Connect to the Flash Chip:
   * Select the chip by pulling the CS (Chip Select) pin low and sending the read command to the flash chip. The command will depend on the specific flash chip you are using (refer to the datasheet for the correct command).
   * For example, to read the contents, you might need to send the read command followed by the address you want to read from.
8.  Read Data from the Flash Chip:

    * After sending the appropriate command and address, use the command to read back the data. You might enter something like:

    ```plaintext
    r  (to read data)
    ```
9. Save the Data:
   * Use a command to save the read data to a file. You may need to copy the output from the terminal manually or check if there's a direct command (this can vary depending on the Bus Pirate firmware).
10. Exit:

    * To exit the Bus Pirate session, type:

    ```plaintext
    q
    ```

## **Resources**

*[Bus Pirate](https://www.flashrom.org/supported\_hw/supported\_prog/buspirate.html)
*[Bus Pirate menu options guide](http://dangerousprototypes.com/docs/Bus\_Pirate\_menu\_options\_guide)
*[Bus Pirate I/O Pin Descriptions](http://dangerousprototypes.com/docs/Bus\_Pirate\_I/O\_Pin\_Descriptions)
