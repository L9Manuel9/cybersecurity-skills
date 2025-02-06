# Port Scanning with Nmap

## Objective/Overview
To find listening services, operating systems, and possible points of entry, do port scans on target systems or networks.

## Tools & Techniques
- Nmap (using -sS, -sV, and -A, among other scan types)
- familiarity with TCP/IP and fundamental networking

## Implementation Steps
1. Use nmap -sS <target> to do a stealth SYN scan in order to rapidly list all open ports.
2. Services operating on discovered ports can be identified by using service version detection (nmap -sV).
3. For further in-depth information, use -A to enable OS detection and script scanning.
4. Keep track of every open port and related service for later use or examination.

## Key Takeaways
- Crucial to penetration testing's reconnaissance process.
- By concentrating on well-known or uncommon services, it aids in identifying possible weaknesses.

TryHackMe: https://tryhackme.com/r/module/nmap


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Network Packet Analysis

## Objective/Overview

Capture and examine unprocessed network data to find irregularities, questionable trends, or weak spots in data streams.

## Tools & Techniques
- To examine packets in depth visually, use Wireshark.
- To quickly collect command line packets, use tcpdump
- Familiarity about TCP, UDP, DNS, HTTP, and other protocols

## Implementation Steps
1. On the selected interface, start Wireshark or tcpdump. Turn on promiscuous mode when necessary.
2. Set up filters, such tcp.port == 80, to target certain traffic.
3. Look for anomalies or unencrypted credentials in the packet contents..
4. For offline analysis and future reference, save.pcap files.

## Key Takeaways
- Reveals cleartext credentials and insecure protocols in use.
- The analysis assists in identifying harmful traffic patterns and diagnosing network issues.

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
