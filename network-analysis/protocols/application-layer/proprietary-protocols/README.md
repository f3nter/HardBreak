# Proprietary Protocols

## Theory

Proprietary protocols are custom communication standards developed by companies to maintain control over their systems and ensure compatibility within their products. These protocols are especially common in IoT devices, where manufacturers often create proprietary solutions to streamline device communication, optimize power and bandwidth, or differentiate their products. However, the closed-source nature of these protocols limits external review, making them harder to analyze and a common target for pentesters. Familiarity with reverse engineering and protocol analysis tools is essential for examining proprietary protocols, which may rely on unique data encodings, custom headers, or non-standard ports.



## Usage

General steps to analyze unknown protocols:

* Capture network traffic from the hub
  * Isolate traffic using a network filter to capture packets only between the hub and its connected devices.
* Analyze protocol behavior
  * Use _Wireshark_ to observe packet structure, data fields, and any encryption.
  * Identify repetitive patterns or clear-text data, indicating weak encryption.
* Reverse engineer the protocol
  * Create a custom dissector in Wireshark or use Python with Scapy to break down the packet structure.
  * Attempt to recreate protocol commands based on observed packet responses.
* Validate findings
  * Replay modified packets to the hub, testing for unhandled commands, buffer overflow vulnerabilities, or bypassed authentication.

## Resources

* [Network Protocol Analysis: The Art of Decoding Digital Footprints](https://sushantkatare.medium.com/network-protocol-analysis-the-art-of-decoding-digital-footprints-17638ed08343)
*  Jingliang Xue et al  [Classification and identification of unknown network protocols based on CNN and T-SNE (PDF)](https://iopscience.iop.org/article/10.1088/1742-6596/1617/1/012071/pdf)
