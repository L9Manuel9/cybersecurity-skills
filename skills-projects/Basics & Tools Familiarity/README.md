Those are my best friends, and we remaing always in touch to know each other better, I'm confident time gonna serve in masterizing this our relationship at best.

# Metasploit Basics

## Objective/Overview

Familiarize yourself with the Metasploit Framework to quickly find and exploit known vulnerabilities.

## Tools & Techniques

- Metasploit modules (auxiliary, exploit, post)
- msfconsole for interactive usage
- Exploit/Payload selection (windows/meterpreter, etc.)

## Implementation Steps

1. Start msfconsole and identify a target or known vulnerability.
2. Search for a suitable exploit module with search <keyword>.
3. Configure the module (RHOST, LHOST, target info) and run exploit.
4. Once you have a session (Meterpreter or shell), escalate privileges or pivot as needed.

## Key Takeaways

- Modular approach speeds up the process from discovery to exploitation.
- One of the most widely used frameworks for professional penetration tests.

TryHackMe: https://tryhackme.com/r/module/metasploit
------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
# Burp Suite Basics

## Objective/Overview 

Learn to use Burp Suite for web security tests through request interception or modification.

## Tools & Techniques

- Proxy interception, Repeater, Intruder
- The Extender adds plugins to Burp
- SSL certificate setup to check HTTPS traffic

## Implementation Steps

1. Set browser proxy to 127.0.0.1:8080.
2. Intercept web requests to check headers, parameters and cookies.
3. Use Repeater to manually test endpoints and manipulate data.
4. Automate fuzzing or brute forcing with Intruder.

## Key Takeaways

- A must-have tool for web app pentesting.
- Makes a full platform to test apps by hand or script.

TryHackMe: https://tryhackme.com/r/module/learn-burp-suite
