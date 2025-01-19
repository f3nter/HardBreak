---
icon: magnifying-glass-chart
---

# Analyze Firmware

After you successfully obtained a firmware dump, it's time to analyze its content.

## **Quick wins**

binwalk is the goto option for quickly analyzing your firmware

* Identify data
  * `binwalk firmware.bin` : will give you an overview which contents are found in the dump
  *   **Example Output:**

      ```bash
      DECIMAL       HEXADECIMAL     DESCRIPTION
      --------------------------------------------------------------------------------
      0             0x0             U-Boot bootloader image, header size: 64 bytes, load address: 0x80800000, entry point: 0x80800000, CRC32: 0xFFFFFFFF
      64            0x40            LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 524288 bytes
      1024          0x400           Linux kernel ARM boot executable zImage (little-endian)
      1048576       0x100000        Squashfs filesystem, little endian, version 4.0, compression: lzma, size: 262144 bytes, 1198 inodes, blocksize: 131072 bytes, created: Mon Jan  1 00:00:00 2024
      ```
*   Extract Firmware

    * `binwalk -e firmware.bin` : will try to automatically extract all content => will often give us full root-filesystem.&#x20;
    * Example:

    <figure><img src="../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Example extraction of a firmware</p></figcaption></figure>
*   Entropy Analyiss

    * `binwalk -E firmware.bin`This will give us the entropy of the firmware
      * Note: parts of very high entropy can be sign for compression or encryption being used.
      * &#x20;Example Output:

    <figure><img src="../.gitbook/assets/image (47).png" alt="" width="375"><figcaption><p>Here we see a blob which might be encrypted or compressed<br><br><br></p></figcaption></figure>

The `strings` command can be helpful to quickly find sensitive data like passwords or password hashes:

*   **Password Hashes:**

    ```bash
    strings firmware.bin | grep -E ':[x$1$5$6]:'
    ```
*   **Hardcoded Credentials**

    ```bash
    strings firmware.bin | grep -i 'password'
    strings firmware.bin | grep -i 'user'
    strings firmware.bin | grep -i 'admin'
    strings firmware.bin | grep -i 'login'
    ```
*   **Private Keys and Certificates**

    ```bash
    strings firmware.bin | grep -i 'PRIVATE KEY'
    strings firmware.bin | grep -i 'BEGIN RSA'
    strings firmware.bin | grep -i 'BEGIN DSA'
    ```
*   **API Keys, Tokens, and Secrets**

    ```bash
    strings firmware.bin | grep -i 'api_key'
    strings firmware.bin | grep -i 'token'
    strings firmware.bin | grep -i 'secret'
    ```
*   **IP Addresses and URLs**

    ```bash
    strings firmware.bin | grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}'
    strings firmware.bin | grep -E 'http://|https://'
    strings firmware.bin | grep -i 'ftp'
    ```
*   **Configuration Files**

    ```bash
    strings firmware.bin | grep -i '.conf'
    strings firmware.bin | grep -i '.ini'
    strings firmware.bin | grep -i '.xml'
    ```
*   **Encryption Keys and Passwords**

    ```bash
    strings firmware.bin | grep -i 'encryption_key'
    strings firmware.bin | grep -i 'aes'
    strings firmware.bin | grep -i 'des'
    strings firmware.bin | grep -i 'key='
    ```
*   **Version Information**

    ```bash
    strings firmware.bin | grep -i 'version'
    strings firmware.bin | grep -i 'build'
    ```
*   **Debug Information**

    ```bash
    strings firmware.bin | grep -i 'debug'
    strings firmware.bin | grep -i 'trace'
    strings firmware.bin | grep -i 'error'
    strings firmware.bin | grep -i 'fail'
    ```
*   **Email Addresses**

    ```bash
    strings firmware.bin | grep -E '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b'
    ```
*   **Encryption/Decryption Routines**

    ```bash
    strings firmware.bin | grep -i 'openssl'
    strings firmware.bin | grep -i 'encrypt'
    strings firmware.bin | grep -i 'decrypt'
    ```
*   **Default and Backup Files**

    ```bash
    strings firmware.bin | grep -i 'default'
    strings firmware.bin | grep -i 'backup'
    ```
*   **SSH Information**

    ```bash
    strings firmware.bin | grep -i 'ssh'
    strings firmware.bin | grep -i 'port'
    ```

## Analysis of bare metal firmware

Todo

Resources:
* [Binwalk: Firmware Analysis Tool](https://github.com/ReFirmLabs/binwalk)
* [Analysing and extracting firmware using Binwalk 3.1.0 in 2025](https://fr3ak-hacks.medium.com/analysing-and-extracting-firmware-using-binwalk-982012281ff6)
* [Reverse engineering my router's firmware with binwalk](https://sergioprado.blog/reverse-engineering-router-firmware-with-binwalk/)