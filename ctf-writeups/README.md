# Capture The Flags

## Publisher [Difficulty: Easy] 
Medium: https://medium.com/@contact_18999/walkthrough-ctf-publisher-4283bd0acfe2 

The "Publisher" CTF machine is a simulated environment hosting some services. Through a series of enumeration techniques, including directory fuzzing and version identification, a vulnerability is discovered, allowing for Remote Code Execution (RCE). Attempts to escalate privileges using a custom binary are hindered by restricted access to critical system files and directories, necessitating a deeper exploration into the system's security profile to ultimately exploit a loophole that enables the execution of an unconfined bash shell and achieve privilege escalation.

- I've Choosen this CTF to made a writeup, Because even if it Easy, It Shows the methodology for most Easy boot-to-root machines.

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
#

## Hammer [Difficulty: Medium]
Medium: https://medium.com/@contact_18999/walkthrough-ctf-hammer-03c366c93006

The "Hammer" CTF challenge presents a vulnerable web application running on an Apache server. Through a series of enumeration techniques—ranging from Nmap scans on ports 22 and 1337 to directory fuzzing and manual investigation—a PhpMyAdmin interface and an hmr_logs directory were uncovered, revealing a critical email address in the error.logs file. By exploiting the application's flawed password reset mechanism, which permitted brute-forcing the 4-digit reset code and bypassing the rate limit, we successfully gained user access and obtained the first flag. Further examination and manipulation of the JWT token allowed us to escalate privileges to an admin role, enabling arbitrary command execution under the www-data user and ultimately securing the second flag located at /home/ubuntu.flag.txt.

- This CTF as part of the "Authentication" module, showcase part of the Analysis process of login forms. + I've enjoyed it.
