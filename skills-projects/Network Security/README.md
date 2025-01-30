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
