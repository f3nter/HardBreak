# Chip readers and programmers

Chip readers and programmers  allow users to read, write, and manipulate the data stored in various types of integrated circuits (ICs), such as microcontrollers, EEPROMs, flash memory, and more. These tools are crucial for tasks like firmware extraction, reverse engineering, and device recovery.

## **Usage**

* Firmware Extraction
  * Reading the firmware from a microcontroller or flash chip to analyze its functionality or vulnerabilities.
* Programming
  * Writing new firmware or configuration data to a chip.
* Device Recovery
  * Restoring corrupted or erased firmware to a functional state.
* Testing and Validation
  * Verifying the integrity of data in chips and ensuring proper functionality.

## **Theory**

* Reading
  * Chip readers utilize specific protocols (such as SPI, I2C, or JTAG) to communicate with the target IC, extracting data stored in memory.
* Programming
  * Programmers send instructions to the chip to write new data, which may involve erasing existing content before programming.
* Types of Memory
  * Different types of memory chips (e.g., EEPROM, flash, PROM) have varying protocols and methods for reading/writing.

Models:

* Entry-Level
  * CH341A USB Programmer(<$15) : very cheap one, flashrom compatible,
* Mid-Range
  * XGecu T56 ($200) or T48 ($80): Frequently used by myself, very reliable, supports a lot of devices, NAND, SPI, eMMC etc.
* High-End
  * Xeltek Superpro (>$550): very precise, but not really needed if you are not a professional
