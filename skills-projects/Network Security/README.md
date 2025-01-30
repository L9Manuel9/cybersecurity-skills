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
