---
icon: magnifying-glass
---

# Reconnaissance

## Theory

Testing a hardware device over Ethernet helps assess network vulnerabilities, intercept sensitive data, and identify exposed services or misconfigurations. This is especially useful for hardware devices that connect to the network, like IoT devices, routers, and industrial equipment.

## Usage

1. Check open ports with nmap:
   1.  A simple Nmap scan can show what services are running on the device:

       ```bash
       nmap <device-ip>  # often devices have a static ip check manual
       ```

       **Example Output:**

       ```bash
       Starting Nmap 7.93 ( https://nmap.org ) at 2024-10-10 14:23
       Nmap scan report for 192.168.1.100
       Host is up (0.00045s latency).
       Not shown: 997 closed ports
       PORT    STATE SERVICE
       22/tcp  open  ssh
       80/tcp  open  http
       443/tcp open  https
       ```
   2. You can also use appropriate flags like:
      1. `-sV`: Version Detection
      2. `-sC`: Default Script Scan
      3. `-A`: Aggressive Scan
      4. `-p-`: Scan All Ports
      5. `-sU`: UDP Scan
      6. `--script vuln` : Runs a vulnerability check
   3. Try common credentials like: admin/admin etc. also google default creds!
2. Webserver available?
   1. Use common tools like `burbsuite`, `gobuster` or `nikto` to identify hidden content or vulnerabilities
   2. There are enough websites who showcase web-pentests, like hacktricks.xzy. Check them out!
   3. You can change configurations?
      1. Explore and experiment, always aiming to enhance access to advanced
3. Firmware Updates!
   1. This is also a very interesting field, as we get the chance to intercept the firmware
   2. Setup:
      1. Setup Wireshark to intercept all traffic from the target device
      2. Start the firmware update
      3. If the firmware is not encrypted, we can recover it from the Wireshark capture
   3. If the firmware is uploaded via FTP, there could be a race condition, where we can download the firmware before it gets deleted from the FTP share
   4. Try to investigate how the firmware update works, and think of how you can intercept it!
   5. Once captured, we can extract password or sensitive data from it

## Resources

* [Nmap webiste](https://nmap.org/)
* [Wireshark website](https://www.wireshark.org/download.html)
