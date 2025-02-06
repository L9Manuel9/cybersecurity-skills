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

- Check required ports access, firmware settings and potentially additional outbound firewall rules
  
3 --------
  
Connecting to the unifi controller through the cloud works just fine. 
Protect I haven't been able to connect to for almost two days now.

--Ample Troubleshooting steps as well as common causes for connection failures--

https://thetechgeeks.com/pages/what-do-i-need-to-run-unifi-protect

https://help.ubnt.com/hc/en-us/articles/360034238233-UniFi-Protect-Troubleshooting-Connectivity

[ ] Note:
Those are in Italian sources, I've usually check in both languages, i woul'd search even in Chinese if i could understand those languages naturally.
1) https://www.raffaelechiatto.com/configurazione-server-openvpn-su-mikrotik-per-accesso-a-devices-nella-lan-interna/
2) https://www.timenet.it/mikrotik-vpn-l2tp-over-ipsec-vpn-vs-pptp-configurazione/
3) https://www.youtube.com/watch?v=2H4sSNZ4wK0


Now, i Feel confident enough. Let's make hands dirty.


## Technical Troubleshooting

Let's Proceed Systematically. So frist let's Tell our client if he was able to Hard power reboot the device and if it was Okay to potentially lose the Video of the camera meanwhile.

Then i Connected from the Client Desktop as discussed to the Console UniFi OS Console, and Again Let's make a Reboot from here. 
So, Since we are in the same managed WiFi, let's connect via the internet browser and Enter the console's IP address into your web browser. 
This address is displayed on the console's LCM screen (for most users, it is 192.168. 1.1)

After this Initial approach, who could have potentially strenghten the device already, since very rarely they get even rebooted.

Let's going deeper.

Check Firewalls & ISP Restrictions

DNS works using UDP Port 53. Ensure that this is not being blocked by any upstream firewalls, gateways or ISP modems. If it is, DNS resolution will fail.

Temporarily disable any custom firewall rules and verify WebRTC traffic is not blocked.


Re-Configuring Your DNS Server
UniFi Cloud Gateways

Navigate to UniFi Network > Settings > Internet > DNS Server and enter the new DNS Server.
CloudKeys, Network Video Recorders & Other Non-Gateway Consoles

Navigate to UniFi OS > Console Settings and check if the IP Configuration is set to DHCP or Static.

    If it is Static, enter the new DNS Server and select Apply Changes.
    If it is DHCP, you will need to modify the DNS Server directly from your DHCP server.
        If you have a UniFi gateway, this is found in UniFi Network > Settings > Networks > [Network Name] > DHCP Service Management > DNS Server.
        Note: This change will take effect after your device’s DHCP lease expires, usually after 24 hours. To expedite this, turn your device off and back on again.

        So let's Reboot again! (It is definetly troubleshooting time, isn't it?)


Let's connect via Winbox to the MikroTik Router.

1. Checked the Firewalls rules and potentially required port access, Everything was ok.
2. Lastly i've updated the Firmware settings with the Auto upgrade method
   System > Packages > Check for Updates . Proceed and then
   System > RouterBOARD > Upgrade.
   Now let's reboot to install the settings.
   System > Reboot

   Connected again, Checked for further updates. And Everything is now updated.


After conducting the initial Troubleshooting phase, i Think we can now Proceed with Adding the VPN to this site. 
I've read it also fixes some problematics and enhance the stability. So it is perfectly tailored for us. Good job client! 
We gain in both security and stability.

VPN L2TP over IPsec client to site: Come configurarlo su MikroTik



   


