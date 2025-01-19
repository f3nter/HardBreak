# flashrom

## Theory

Flashrom is an open-source tool used for reading, writing, verifying, and erasing flash memory chips. It supports a wide range of chipsets and is primarily used for flashing BIOS, firmware, and embedded systems. Flashrom is essential for penetration testers and hardware hackers, as it enables low-level access to the firmware of devices, allowing for potential vulnerabilities to be identified and exploited.

#### Key Features

* Cross-Platform
  * Available on Linux, Windows, and macOS.
* Wide Chip Support
  * Compatible with various flash chips and devices.
* Read/Write Operations
  * Allows for easy backup and flashing of firmware.
* Verification
  * Ensures that the flashing process was successful by comparing the written data with the source.
* Live Flashing
  * Can be used to flash a system while it is running.

## Cheat Sheet

```bash
# Install Flashrom on Linux
sudo apt-get update
sudo apt-get install flashrom

# Install Flashrom on macOS (using Homebrew)
brew install flashrom

# Detect the flash chip on your device
sudo flashrom -p <programmer>

# Example with Bus Pirate
flashrom -p buspirate_spi:dev=/dev/ttyUSB0,spispeed=1M

# Read flash memory and save it to a file
sudo flashrom -p <programmer> -r backup.bin

# Write a new firmware image to the flash chip
sudo flashrom -p <programmer> -w firmware.bin
```

### Installation

To install Flashrom on different platforms, you can follow these commands:

{% tabs %}
{% tab title="Linux" %}
```bash
sudo apt-get update
sudo apt-get install flashrom
```
{% endtab %}

{% tab title="OSX" %}
Here are the instructions for macOS using Homebrew

```bash
brew install flashrom
```
{% endtab %}

{% tab title="Windows" %}
#### Installation Steps

1. **Download Flashrom**:
   * Visit the [Flashrom Releases page on GitHub](https://github.com/flashrom/flashrom/releases) and download the latest `.zip` file for Windows.
2. **Extract the Zip File**:
   * After downloading, extract the contents of the `.zip` file to a directory of your choice.
3. **Set Up Environment**:
   * Open Command Prompt and navigate to the directory where you extracted Flashrom.
   * You may need to add the directory to your system's `PATH` environment variable for easier access.

#### Example Commands

If you want to use it directly without adding it to your PATH, you can navigate to the directory where Flashrom is located. For example, if you extracted it to `C:\flashrom`, you would use:

```bash
cd C:\flashrom
```

Then run Flashrom with the following command:

```bash
flashrom -p internal
```
{% endtab %}
{% endtabs %}

## Usage

#### Detecting the Chip

To detect the flash chip on a device, use:

```bash
sudo flashrom -p <programmer>
```

Replace `<programmer>` with the appropriate programmer (e.g., `linux_spi`, `internal`, etc.).

Example Bus Pirate:

```bash
flashrom -p buspirate_spi:dev=/dev/ttyUSB0,spispeed=1M
```

#### Reading the Flash

To read the flash memory and save it to a file:

```bash
sudo flashrom -p <programmer> -r backup.bin
```

#### Writing to the Flash

To write a new firmware image to the flash:

```bash
sudo flashrom -p <programmer> -w firmware.bin
```

## Expected Output

When the command executes successfully, you might see output similar to the following:

```vbnet
Flashrom v1.2.3-r1234 on Linux 5.4.0-74-generic (x86_64), built with libpci 3.6.4, gcc 9.3.0, little endian
   
Calibrating delay loop... OK.
Detected chipset: Intel H61
Found chip "W25Q64.V" (8192 KB, SPI) at physical address 0x00000000.
Reading flash... done.
Size: 8192 KB
Saved to backup.bin
```

### Important Notes

* Always ensure you have a valid backup of the current firmware before attempting to flash a new image.
* Incorrectly flashing firmware can lead to bricking the device, making it inoperable.
* Consult the Flashrom documentation for more detailed information and supported hardware.

## Resources

* [Flashrom website](https://www.flashrom.org/)
* [Flashrom Git repository](https://github.com/flashrom/flashrom)
