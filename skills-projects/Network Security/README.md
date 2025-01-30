# Port Scanning with Nmap

## Objective/Overview
Conduct port scans on target systems or networks to identify listening services, operating systems, and potential points of entry.

## Tools & Techniques
- Nmap (using various scan types, such as `-sS`, `-sV`, and `-A`)
- Knowledge of TCP/IP and basic networking

## Implementation Steps
1. Run a stealth SYN scan (`nmap -sS <target>`) to quickly enumerate open ports.
2. Use service version detection (`nmap -sV`) to identify services running on discovered ports.
3. Enable OS detection and script scanning with `-A` for deeper insights.
4. Document each open port and associated service for subsequent exploitation or analysis.

## Key Takeaways
- Essential for reconnaissance in penetration testing.
- Helps narrow down potential vulnerabilities by focusing on known or unusual services.

TryHackMe: https://tryhackme.com/r/module/nmap


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Network Packet Analysis

## Objective/Overview

Capture and examine raw network traffic to detect anomalies, suspicious patterns, or vulnerabilities within the data flow.

## Tools & Techniques
- Wireshark for in-depth graphical packet analysis
- tcpdump for quick, command-line captures
- Familiarity with network protocols (TCP, UDP, DNS, HTTP, etc.)

## Implementation Steps
1. Launch Wireshark or tcpdump on the target interface, enabling promiscuous mode if appropriate.
2. Apply filters (e.g., tcp.port == 80) to focus on relevant traffic.
3. Inspect packet contents for unencrypted credentials or anomalies.
4. Save capture files (.pcap) for offline review and documentation.

## Key Takeaways
- Reveals cleartext credentials and insecure protocols in use.
- Useful for troubleshooting network issues and identifying malicious traffic patterns.

TryHackMe: https://tryhackme.com/r/module/wireshark
& https://tryhackme.com/r/room/tcpdump


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# MAC Address Spoofing

## Objective/Overview
Demonstrate how changing one’s MAC address can bypass basic network filters or gain conditional access to systems that rely on MAC-based restrictions.

## Tools & Techniques
- ifconfig or ip link on Linux-based systems
- macchanger for automated/random MAC generation
- Knowledge of layer 2 (Ethernet) operations

## Implementation Steps
1. Bring down the network interface (`ifconfig eth0 down`).
2. Use macchanger to set a random or specific MAC address (`macchanger -r eth0`).
3. Bring the interface back up (`ifconfig eth0 up`) and verify the new MAC address.
4. Test connectivity or bypass MAC-based security controls if they exist.

## Key Takeaways
- Highlights the weakness of MAC-based security mechanisms.
- More robust solutions (e.g., 802.1X) are necessary to prevent spoofing attacks.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Basic Firewall Evasion Techniques

## Objective/Overview
Learn ways to bypass simple firewall rules or basic network filtering, simulating adversarial tactics used to penetrate restricted networks.

## Tools & Techniques
- Fragmented packets or packet crafting
- Tunneling protocols (HTTP/S, SSH, VPN)
- Using non-standard ports or proxychains

## Implementation Steps
1. Identify open ports or allowed services on the target network (e.g., port 443).
2. Attempt to disguise malicious traffic within commonly allowed protocols (e.g., HTTPS).
3. Use tools like proxychains or SSH tunnels to route scans or exploitation traffic.
4. Document which evasion methods succeeded or failed against the firewall configuration.

## Key Takeaways
- Illustrates the arms race between attacker methods and defensive technologies.
- Encourages monitoring lateral movement and performing strict egress filtering.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# ARP Poisoning and MITM Attack

## Objective/Overview
Intercept traffic between hosts in a local network by tampering with the Address Resolution Protocol (ARP) cache, allowing man-in-the-middle (MITM) attacks.

## Tools & Techniques
- Tools such as arpspoof, ettercap, or Bettercap
- Enabling IP forwarding on the attacker’s machine
- Knowledge of ARP caching mechanisms

## Implementation Steps
1. Identify target IPs (victim and gateway).
2. Use arpspoof or bettercap to send false ARP replies to both targets.
3. Enable IP forwarding to relay packets and maintain connectivity.
4. Capture or modify traffic passing through your system for further analysis or injection.

## Key Takeaways
- Demonstrates the inherent insecurity of ARP in LAN environments.
- Strongly reinforces the need for encrypted communications (HTTPS, SSH) on local networks.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Network Mapping with Netdiscover

## Objective/Overview
Quickly map live hosts on a local network and identify their MAC addresses, often used for initial reconnaissance in a LAN environment.

## Tools & Techniques
- Netdiscover in active or passive mode
- ARP scanning and MAC address lookup
- Familiarity with OS fingerprinting or layer 2 networking

## Implementation Steps
1. Set up netdiscover with a target range (`netdiscover -r 192.168.1.0/24`).
2. Collect the list of active IPs, associated MAC addresses, and device manufacturers.
3. Save or document these findings for targeted scans (e.g., Nmap, vulnerability scans).
4. (Optional) Use results to identify rogue devices or unknown hosts.

## Key Takeaways
- Provides a quick overview of connected devices in the network.
- Essential before deeper vulnerability scanning or exploitation.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Packet Sniffing with Scapy

## Objective/Overview
Use Scapy, a powerful Python library, to capture, analyze, and craft custom packets for advanced network testing and research.

## Tools & Techniques
- Scapy for Python-based packet manipulation
- Basic understanding of TCP/IP headers and packet structures
- Potential for forging or fuzzing network traffic

## Implementation Steps
1. Install Scapy (`pip install scapy`).
2. Run sniffing functions (`sniff()`) to capture traffic based on specified filters.
3. Parse captured packets, extract fields (e.g., IP, TCP, DNS).
4. Build and send custom packets (`sendp()`, `send()`) for testing or fuzzing.

## Key Takeaways
- Ideal for deep protocol analysis and building custom packets.
- Encourages experimenting with network traffic in a controlled, authorized environment.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
