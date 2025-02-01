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
# DNS Enumeration

## Objective/Overview 

Uncover DNS records that can reveal subdomains, mail servers, or other infrastructure details about a target.

## Tools & Techniques

- dnsenum, dig, nslookup
- Zone transfers (if misconfigured)
- Subdomain brute forcing

## Implementation Steps

1. Use dig or nslookup to query for A, MX, NS, CNAME records.
2. Attempt a zone transfer (dig AXFR @nameserver domain.com) if allowed.
3. Run dnsenum or other scripts to systematically find subdomains.
4. Document your findings for potential entry points or infrastructure mapping.

## Key Takeaways
 
- Often reveals hidden or staging subdomains.
- Reiterates the importance of proper DNS configuration to prevent zone transfers.

TryHackMe: https://tryhackme.com/r/room/passiverecon

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Understanding Cookies and Sessions

## Objective/Overview 

Investigate how web sessions work, including cookie-based authentication and possible session hijacking methods.

## Tools & Techniques

- Browser dev tools, Burp Suite
- Inspecting Set-Cookie headers
- Session fixation or hijacking concepts

## Implementation Steps

1. Log in to a test web application, note the session ID in cookies.
2. Observe how the session ID changes upon logout or different flows.
3. Attempt to reuse the same cookie from another browser or device.
4. Document if the application properly invalidates sessions upon logout.

## Key Takeaways

- Essential to securing user authentication.
- Without secure cookies, an attacker might hijack sessions for unauthorized access.

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Analyzing Network Logs for Intrusions

## Objective/Overview 

Review firewall, IDS, or server logs to detect suspicious patterns indicating attacks or unauthorized access attempts.

## Tools & Techniques

- Splunk, ELK stack (Elasticsearch, Logstash, Kibana)
- Searching for abnormal traffic patterns (high volume, repeated failures)
- Correlating events across multiple log sources

## Implementation Steps

1. Aggregate logs in a centralized tool (e.g., Kibana) or use command-line parsing (e.g., grep, awk).
2. Search for anomalies—unusual IP addresses, frequent authentication failures.
3. Create dashboards or alerts for repeated suspicious behavior.
4. Investigate suspicious events, cross-referencing with threat intelligence if available.

## Key Takeaways

- Proactive log analysis can detect intrusions early.
- Helps refine security controls and incident response plan

TryHackMe: https://tryhackme.com/r/room/introtosiem & https://tryhackme.com/r/room/idsfundamentals

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

Note: I did it also on my Main desktop. Which is on Qubes 4.2 at Dom0 level, as part of my Initial Anonymizing Procedure.


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

Note: U can Accomplish it using standard tools as Scapy and Nmaps with the right parameters.

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
