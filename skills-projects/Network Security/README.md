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

Capture and inspect raw network data to find anomalies, harmful traffic, or vulnerabilities in data flow.

## Tools & Techniques
- To visually examine packets depthly, use Wireshark.
- To quickly collect packets via command line , use tcpdump
- Understanding TCP, UDP, DNS, HTTP, and other protocols

## Implementation Steps
1. On the selected interface, start Wireshark or tcpdump. Turn on promiscuous mode when necessary.
2. Set up filters, (e.g. tcp.port == 80), to remove noise and target specific traffic.
3. Look for anomalies or unencrypted credentials in the packet contents.
4. For offline analysis and future reference, save .pcap files.

## Key Takeaways
- Reveals cleartext credentials and insecure protocols in use.
- The analysis assists in identifying harmful traffic patterns and diagnosing network issues.

TryHackMe: https://tryhackme.com/r/module/wireshark
& https://tryhackme.com/r/room/tcpdump


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# DNS Enumeration

## Objective/Overview 

Discover DNS records that may provide mail servers, subdomains, or other infrastructure information about a target.

## Tools & Techniques

- dnsenum, dig, nslookup
- Zone transfers (if misconfigured)
- Subdomain brute forcing

## Implementation Steps

1. Use dig or nslookup to query for A, MX, NS, CNAME records.
2. If permitted, attempt a zone transfer (dig AXFR @nameserver domain.com).
3. Use programs such as dnsenum to methodically locate subdomains.
4. Keep track of your discoveries for mapping infrastructure or potential entry points.

## Key Takeaways
 
- Often exposes staging or hidden subdomains.
- Stresses the need of setting up DNS correctly to prevent zone transfers.

TryHackMe: https://tryhackme.com/r/room/passiverecon

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Understanding Cookies and Sessions

## Objective/Overview 

Investigate how web sessions work, including cookie-based authentication and potential techniques for session hijacking

## Tools & Techniques

- Development tools in browsers, Burp Suite
- Looking at the Set-Cookie headers
- Session fixation or hijacking concepts

## Implementation Steps

1. Log in to a test web application, note the session ID in cookies.
2. As you log out or travel through several processes, note how the session ID changes.
3. Try using the identical cookie on a different browser or device.
4. Note if the application properly invalidates sessions upon logout.

## Key Takeaways
 
- Vital to safeguarding user authentication.
- Unauthorized access might be gained by an attacker if secure cookies are not used.

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Analyzing Network Logs for Intrusions

## Objective/Overview 

Examine server logs, firewall, or Intrusion Detection System logs for any unusual patterns that could point to intrusions or illegal access attempts.

## Tools & Techniques

- Splunk with the ELK stack (Logstash, Kibana, and Elasticsearch)
- Looking for unusual traffic patterns, such as high volume or recurring failures
- Linking occurrences from several log sources

## Implementation Steps

1. Logs can be combined in a centralized application (like Kibana) or parsed using command-line tools (like grep and awk).
2. Look for irregularities, such as strange IP addresses or recurring authentication issues.
3. Make alerts or dashboards for persistently questionable activity.
4. Examine suspicious occurrences and, if available, cross-reference with threat intelligence.

## Key Takeaways

- Early intrusion detection is possible with proactive log analysis.
- Helps refine security controls and incident response procedures.

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
- Draws attention to the weakness of MAC-based security mechanisms.
- Stronger solutions (like 802.1X) are required to stop spoofing attempts.

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
Manipulate the Address Resolution Protocol (ARP) cache to intercept communication between hosts in a local network, enabling man-in-the-middle (MITM) attacks. 

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
Rapidly map active hosts on a local area network and get their MAC addresses, which are frequently used for preliminary LAN reconnaissance.

## Tools & Techniques
- Netdiscover in active or passive mode
- ARP scanning and MAC address lookup
- Familiarity with OS fingerprinting or layer 2 networking

## Implementation Steps
1. Set up netdiscover with a target range (`netdiscover -r 192.168.1.0/24`).
2. Collect the list of active IPs, associated MAC addresses, and device manufacturers that are currently in use.
3. Save or document these findings for targeted scans (e.g., Nmap, vulnerability scans).
4. (Optional) Use the findings to identify unknown hosts or rogue devices.

## Key Takeaways
- It gives a quick overview of connected devices in the network.
- Good to do prior deeper vulnerability scanning or exploitation.


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
