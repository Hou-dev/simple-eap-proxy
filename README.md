# Simple EAP proxy

What is an eap proxy?
In computer networking is a server that acts as an intermediary from clients seeking resources from a server that provides those resources. In our case we are requesting eap packets from the ont and sending them to the modem provided by the ATT.

Why use an eap proxy to bypass the ATT modem/router combo?
User friendly GUI for managing network using Ubiquiti EdgeOS
Performance issues with Modem
Easy port forwarding 
Deep Packet Inspection / Traffic Analysis built into EdgeOS
Using and install custom packages into EdgeOS such as HTOP, IPTraf, etc
QoS using smart queue management if your network is running 150 mbps or less instead for 1 gbps

Simple EAP Proxy Setup
Initial Steps
Download and install WinSCP ( https://winscp.net/eng/index.php )
Download and install PuTTY ( https://www.putty.org/ )
Setup Edgerouter X and run basic setup. Make sure you are not running v2.x.x because the proxy only works with v1.x.x
Make note of Modem/Router MAC address. It’s usually on black stick on the side of device
Make a Backup
Once the initial setup of the ER-X is finished, make a backup by click on “System” on the bottom left then clicking “Download”

Transfer
Download the EAP Proxy by going to ( https://github.com/jaysoffian/eap_proxy ) and clicking the the green download button
Login into the ER-X using WinSCP using the SCP protocol. Hit the up arrow on the folder until you are on the root directory
Drag and drop eap_proxy.py to /config/scripts/
Drag and drop eap_proxy.sh.example to /config/scripts/post-config.d/
Rename eap_proxy.sh.example to eap_proxy.sh
PuTTY
Open command in WinSCP and click “open in PuTTY”
Enter password and then type the following commands
sudo chmod +x /config/scripts/eap_proxy.py
sudo chmod +x /config/scripts/post-config.d/eap_proxy.sh

WARNING: This is the most dangerous setup. I am not responsible if you brick your ER-X.
Editing config.boot
Navigate using WinSCP to /config/
Right click on config.boot and hit edit
Scroll down until you see system, then delete everything above it.
Reminder: Do not delete your system code it is where you password is stored
Replace deleted text with code below
Scroll to system and here is where you can change the dns to cloudflare (1.1.1.1) or google (8.8.8.8). Under “name-server” , type your preferred DNS provider
Look for offload and type “hwnat enable” without quotes




Credit
https://github.com/jaysoffian/eap_proxy
https://github.com/Genghis1227/guide_eap_proxy
https://old.reddit.com/r/Ubiquiti/comments/c36ko1/help_with_eap_proxy/

