# Wi-Fi Network Scanning

## Objective/Overview
Discover and map nearby wireless networks, understand their security protocols, signal strength, and potential vulnerabilities.

## Tools & Techniques
- aircrack-ng suite (specifically, airodump-ng)
- Wireless network adapters capable of monitor mode
- Understanding of wireless protocols (802.11)

## Implementation Steps
1. Enable monitor mode on your wireless adapter (`airmon-ng start wlan0`).
2. Use airodump-ng `<monitor_interface>` to list all visible Wi-Fi networks, capturing details such as BSSID, ESSID, channel, and encryption type.
3. Focus on networks of interest by specifying particular channels (`-c`) or BSSIDs.
4. Network details should be documented for following deep analysis or targeted testing.

## Key Takeaways
- The first step in wireless penetration testing, which is essential for the identification of networks with weak or no encryption
- Shows the significance of using safe protocols like WPA2 or WPA3.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Wireless Network Hacking

## Objective/Overview
Identify weaknesses in wireless networks and execute attacks to demonstrate the potential risks associated with poorly secured Wi-Fi setups.

## Tools & Techniques
- aircrack-ng suite (e.g., aircrack-ng, aireplay-ng, airodump-ng)
- Wordlists for WPA/WPA2 password cracking
- WPS vulnerabilities with tools like reaver

## Implementation Steps
1. Capture a 4-way handshake using airodump-ng and aireplay-ng to deauthenticate a client (forcing a re-authentication capture).
2. Use aircrack-ng with a wordlist to attempt to crack the WPA/WPA2 key.
3. Alternatively, use reaver to exploit WPS on networks with WPS enabled.
4. Demonstrate access to previously secured networks and recommend secure configurations.

## Key Takeaways
- The discovery of security weaknesses in networks found that WEP and some WPA/WPA2 networks using WPS are most vulnerable.
- Underlines the need for strong encryption and the disabling of WPS in wireless setups.


------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Using Wi-Fi Pineapple for MITM Attack

## Objective/Overview
Wi-Fi Pineapple allows us to achieve Man-in-the-Middle (MITM), that is done by not only creating a rogue access point but also catching all the data of the victim.

## Tools & Techniques
- Wi-Fi Pineapple hardware device
- Modules for traffic logging, DNS spoofing, and SSL stripping
- Mastering the concepts of rogue AP and network redirection

## Implementation Steps
1. Configure the Wi-Fi Pineapple to mimic legitimate network SSIDs, creating an attractive rogue AP.
2. Execute DNS spoofing and SSL stripping to capture credentials and monitor traffic.
3. Document the types of data captured and the effectiveness of the MITM configuration.
4. Report on potential countermeasures and emphasize user education on avoiding untrusted networks.

## Key Takeaways
- Demonstrates how easily users can be tricked into connecting to rogue networks.
- Reminds us of the fact that the most powerful measure to secure a network is a strict network SSID management and traffic encryption with services like VPNs.



------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Network Recon with Airodump-ng

## Objective/Overview
Use airodump-ng from the aircrack-ng suite to conduct detailed reconnaissance on wireless networks, identifying devices and potential targets.

## Tools & Techniques
- aircrack-ng suite, specifically airodump-ng
- Monitor mode on Wi-Fi adapters
- Analyzing captured network traffic for hidden networks and client associations

## Implementation Steps
1. Start the wireless card in monitor mode and run airodump-ng `<monitor_interface>`.
2. Capture data packets for analysis, recording information on detected wireless networks and client devices.
3. Use filters to target specific channels or BSSIDs for in-depth analysis.
4. Document findings on device types and encryption methodologies in use.

## Key Takeaways
- Provides an overview of wireless networks and their configurations within range.
- Essential reconnaissance step before planning any further penetration or testing efforts.
