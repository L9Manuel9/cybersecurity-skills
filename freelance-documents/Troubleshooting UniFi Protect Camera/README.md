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

verify WebRTC traffic is not blocked.


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

I've read it also fixes some problematics and enhance the stability. 

So it is perfectly tailored for us. Good job client in asking a VPN! We gain in both security and stability.


# Configuring OpenVPN Server on Mikrotik for Access to Devices in the Internal LAN

This tutorial provides a step-by-step guide to configure an OpenVPN server on a Mikrotik router. It also covers firewall configuration to allow VPN clients to access devices on the internal LAN and explains how to set up the OpenVPN client on a PC.

---
Prerequisites
- A Windows PC
- WinBox (download from Mikrotik’s official website)
  - Choose the 32-bit or 64-bit version based on your operating system.
---
## Accessing the Mikrotik Configuration
1. Access the Mikrotik router using WinBox or the web interface (if enabled).
2. Open the Mikrotik Terminal by clicking the “New Terminal” button.

NOTE:   
- You can configure and use the VPN even if the domain and DNS are not publicly accessible.  
- Delays or timeouts may occur when generating certificates. These certificates remain valid for 10 years (3650 days).
---
## Creating the Certificates
Run the following commands to create the necessary certificates for the VPN:

mikrotik

/certificate

add name=ca-template common-name=raffaelechiatto.com days-valid=3650 key-size=4096 key-usage= crl-sign,key-cert-sign

add name=server-template common-name=server.raffaelechiatto.com days-valid=3650 key-size=4096 key-usage= digital-signature,key-encipherment,tls-server

add name=client-template common-name=client.raffaelechiatto.com days-valid=3650 key-size=4096 key-usage= tls-client

---


Signing the Certificates
Sign the certificates using the following commands:


/certificate

sign ca-template name=ca-certificate

sign server-template name=server-certificate ca=ca-certificate

sign client-template name=client-certificate ca=ca-certificate

note:

Some commands may time out during this phase. This is normal—continue with the process.
Verification:  
1. Open the Certificates section in WinBox:  
   Click “System” → “Certificates”.  
2. Ensure the certificates have the following properties:  
   - CA Certificate: *KLAT*  
   - Client Certificate: *KIT*  
   - Server Certificate: *KI*
---
Exporting the Certificates
Export the certificates using these commands:


/certificate

export-certificate ca-certificate export-passphrase=""

export-certificate client-certificate export-passphrase=password12345

-

- Select the files (two certificates and one key) and click “Download”.  
- Save the files to a convenient location (e.g., your desktop).
---
Creating the IP Address Pool
Create an IP address pool for VPN clients:


/ip

pool add name="vpn-pool" ranges= 192.168.8.10-192.168.8.30

verification:

- Go to IP → Pool in WinBox.  
- Ensure the pool is created with the assigned IP range.
---
Configuring the PPP OpenVPN Server
Configure the PPP server to accept VPN connections:


/ppp

profile add name="vpn-profile" use-encryption=yes local-address=192.168.8.250 dns-server=192.168.8.250 remote-address=vpn-pool

secret add name=adminvpn profile=vpn-profile password=password12345

configure


/interface

ovpn-server server

set default-profile=vpn-profile certificate=server-certificate require-client-certificate=yes auth=sha1 cipher=aes128,aes192,aes256 enabled=yes

---


Firewall Configuration
Allow VPN clients to access the LAN:
### Firewall Filter Rules


/ip firewall filter

add chain=forward connection-state=established,related,untracked action=accept comment="Accept forwarding for established and related connections"

add chain=forward src-address=192.168.8.0/24 action=accept comment="Allow forwarding from OVPN clients"

add chain=input connection-state=established,related,untracked action=accept comment="Accept input for established and related connections"

add chain=input protocol=tcp dst-port=1194 action=accept comment="Allow OpenVPN connection"

add chain=input in-interface=all-ppp action=accept comment="Allow input from OVPN clients"

add chain=input protocol=tcp dst-port=8291 action=accept comment="Allow Winbox input"

add chain=input protocol=tcp dst-port=443 action=accept comment="Allow HTTPS"

add chain=input action=drop comment="Drop all other connections"

add chain=forward action=drop comment="Drop forward for all other connections"

add chain=forward connection-state=invalid action=drop comment="Drop invalid connections"

## NAT


/ip firewall nat

add chain=srcnat src-address=192.168.8.0/24 action=masquerade comment="Allow VPN clients to browse the Internet through the cloud/server network"

---


Creating the .ovpn Configuration File
Create a file called client.ovpn on your PC and add the following content:


client

dev tun

proto tcp

remote IP_PUBLIC 1194

resolv-retry infinite

nobind

persist-key

persist-tun

ca ca.crt

cert client.crt

key client.key

remote-cert-tls server

cipher AES-128-CBC

auth SHA1

auth-user-pass

redirect-gateway def1

verb 3


note:
Replace IP_PUBLIC with the public IP address or DNS name of the Mikrotik router.
---
OpenVPN Client Configuration
1. Download and install the OpenVPN client from OpenVPN Community Downloads.  
   - Always download the latest version available.  
2. Copy the following files to the folder C:\Program Files\OpenVPN\config:  
   - ca.crt  
   - client.crt  
   - client.key  
   - client.ovpn  
3. Launch the OpenVPN client, click the icon in the system tray, and select “Connect”.  
4. Enter the username and password you created earlier to establish the VPN connection.
---
## Split-Tunnel OpenVPN Configuration
A split tunnel routes specific traffic through the VPN while leaving the rest unaffected.
### Steps to Configure Split Tunneling:
1. Find the IP address of the website(s) you want to route through the VPN using nslookup or an IP lookup tool (e.g., XMyIP).  
2. Edit the .ovpn configuration file and add the following lines:  
   

route-nopull

route [website IP address] 255.255.255.255


To Remove Split Tunneling:
Delete the above two lines from the .ovpn file and restart the VPN connection.
TIP:  
Configure DNS servers in the VPN to prevent DNS leaks.
---
Thank you for reading! ❤️




   


