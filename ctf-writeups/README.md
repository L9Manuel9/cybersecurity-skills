# Capture The Flags

## Publisher [Easy]
Medium Walkthrough: https://medium.com/@contact_18999/walkthrough-ctf-publisher-4283bd0acfe2

The "Publisher" CTF machine is a simulated environment hosting some services. Through a series of enumeration techniques, including directory fuzzing and version identification, a vulnerability is discovered, allowing for Remote Code Execution (RCE). Attempts to escalate privileges using a custom binary are hindered by restricted access to critical system files and directories, necessitating a deeper exploration into the system's security profile to ultimately exploit a loophole that enables the execution of an unconfined bash shell and achieve privilege escalation.

------------------------------------------------------------------------------0101010101---0101010101---0101010101---010101010
