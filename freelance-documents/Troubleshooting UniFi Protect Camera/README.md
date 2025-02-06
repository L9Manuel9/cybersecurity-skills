# Troubleshooting & VPN Implementation

## System: UniFi Protect (Camera)
#### Connected to a network managed by a: MikroTik Cloud Core Router
##### With a dedicated VLAN.

#### Issue: The Internet is working properly, but there are occasional disconnections that make the UniFi Protect system unreachable from the outside

#### Hypothesis: Client suggests it may be a problem related to some firewall rule on MikroTik

#### Request: Checking the Firewall on MikroTik

#### Further Request: Configure a VPN on the MikroTik in order to be able to  remotely access the UniFi Protect system securely.


Let's begin with this scenario. After an initial preparation and a quick call with my Client i'd started to working from his desktop via anydesk 
with the proper privileges in order to smoothly fix this issue, but frist. let's return at the moment before starting my work.

Frist off all, I've documented myself properly, I've solid fundamentals in both Networking & IoT devices, that's why i accepted to handle this.
However i was lacking of knowledge specifically in UniFi Protect devices and MikroTik Cloud Core Router platform.

Let's remediate, make searches and gather information about Specifically.

## That's Directly from my Notepad.

--Approaches to test--

I had the same problem yesterday with UDM SE. It could not be accessed from the outside via Site Manager. 
Local login via Site Manager with a VPN connection was successful, as was local login straight to the console. 
I Disabled/re-enabled remote access on my UDM SE. That did not help. Then I restarted UDM SE. 
Since then it has been accessed normally from the outside via Site Manager.

- Was able to rectified via a hard power reboot

2 -------- 

Have the same issue here. UDM Pro SE.

Update: Looks like restarting my UDM did the trick (both for alarms and connecting outside my LAN)

- Rebooting the console resolved the issue. 

--Section2--

Depending on your internet service provider (provided modem router) it be blocking required ports to access the Cloud Key. 
If you are able to review the firmware settings and ensure that no additional outbound firewall rules are preventing access

- Check this
  
3 --------
  
Connecting to the unifi controller through the cloud works just fine. 
Protect I haven't been able to connect to for almost two days now.

--Ample Troubleshooting steps as well as common causes for connection failures--

https://help.ubnt.com/hc/en-us/articles/360034238233-UniFi-Protect-Troubleshooting-Connectivity

[ ] Note:
Those are in Italian sources, I've usually check in both languages, i woul'd search even in Chinese if i could understand those languages naturally.
1) https://www.raffaelechiatto.com/configurazione-server-openvpn-su-mikrotik-per-accesso-a-devices-nella-lan-interna/
2) https://www.timenet.it/mikrotik-vpn-l2tp-over-ipsec-vpn-vs-pptp-configurazione/
3) https://www.youtube.com/watch?v=2H4sSNZ4wK0


Now, i Feel confident enough. Let's make hands dirty.


## Technical Troubleshooting


