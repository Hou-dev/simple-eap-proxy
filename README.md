## What is an eap proxy?

In computer networking is a server that acts as an intermediary from clients seeking resources from a server that provides those resources. In our case we are requesting eap packets from the ont and sending them to the modem provided by the ATT.

## Why use an eap proxy to bypass the ATT modem/router combo?

- User friendly GUI for managing network using Ubiquiti EdgeOS
- Performance issues with Modem
- Easy port forwarding 
- Deep Packet Inspection / Traffic Analysis built into EdgeOS
- Using and install custom packages into EdgeOS such as HTOP, IPTraf, etc
- QoS using smart queue management if your network is running 150 mbps or less instead for 1 gbps

## Simple EAP Proxy Setup

 **1. Initial Steps**

- Download and install WinSCP ( https://winscp.net/eng/index.php )
![Annotation 2020-06-04 161400](https://user-images.githubusercontent.com/59487209/83816356-d904fd00-a687-11ea-9ef8-88c8180d6d4d.png)
- Download and install PuTTY ( https://www.putty.org/ )
![Annotation 2020-06-04 161841](https://user-images.githubusercontent.com/59487209/83816408-f1751780-a687-11ea-8352-d5c8af206b39.png)
- Make note of Modem/Router MAC address. It’s usually on black stick on the side of device
- Setup Edgerouter X and run basic setup. Make sure you are not running v2.x.x because the proxy only works with v1.x.x
![Annotation 2020-06-04 161324](https://user-images.githubusercontent.com/59487209/83816307-b672e400-a687-11ea-9748-4b050598fc8c.png)
- Make a Backup
- Once the initial setup of the ER-X is finished, make a backup by click on “System” on the bottom left then clicking “Download”
![Annotation 2020-06-04 161446](https://user-images.githubusercontent.com/59487209/83816459-0b165f00-a688-11ea-936e-9cdc13c14407.png)

**2. Transfer**

- Download the EAP Proxy by going to ( https://github.com/jaysoffian/eap_proxy ) and clicking the the green download button
![Annotation 2020-06-04 161658](https://user-images.githubusercontent.com/59487209/83816513-2f723b80-a688-11ea-89c9-ebed80566202.png)
- Login into the ER-X using WinSCP using the SCP protocol. Hit the up arrow on the folder until you are on the root directory
![Annotation 2020-06-04 162044](https://user-images.githubusercontent.com/59487209/83816600-5d578000-a688-11ea-855d-3c8308c10608.png)
- Drag and drop eap_proxy.py to /config/scripts/
- Drag and drop eap_proxy.sh.example to /config/scripts/post-config.d/
- Rename eap_proxy.sh.example to eap_proxy.sh

![Annotation 2020-06-04 162431](https://user-images.githubusercontent.com/59487209/83816681-955ec300-a688-11ea-910c-ed3461dacafc.png)

**3. PuTTY**

Open command in WinSCP and click “open in PuTTY”

![Annotation 2020-06-04 162653](https://user-images.githubusercontent.com/59487209/83816739-b3c4be80-a688-11ea-82be-7e73fb5f76bb.png)

Enter password and then type the following commands

    sudo chmod +x /config/scripts/eap_proxy.py
    sudo chmod +x /config/scripts/post-config.d/eap_proxy.sh

**WARNING: This is the most dangerous setup. I am not responsible if you brick your ER-X.**

 **4. Editing config.boot**

- Navigate using WinSCP to /config/
- Right click on config.boot and hit edit

![Annotation 2020-06-04 163810](https://user-images.githubusercontent.com/59487209/83816868-01d9c200-a689-11ea-8e17-bab02d1deb8c.png)

- Scroll down until you see system, then delete everything above it
**Reminder: Do not delete your system code it is where you password is stored**
- Replace deleted text with code below
- Scroll to system and here is where you can change the dns to cloudflare (1.1.1.1) or google (8.8.8.8). Under “name-server” , type your preferred DNS provider
- Look for offload and type “hwnat enable” without quotes

![Annotation 2020-06-04 174210](https://user-images.githubusercontent.com/59487209/83817602-cdff9c00-a68a-11ea-861d-6097480ad0a3.png)


## Credit

[https://github.com/jaysoffian/eap_proxy](https://github.com/jaysoffian/eap_proxy)

[https://github.com/Genghis1227/guide_eap_proxy](https://github.com/Genghis1227/guide_eap_proxy)

[https://old.reddit.com/r/Ubiquiti/comments/c36ko1/help_with_eap_proxy/](https://old.reddit.com/r/Ubiquiti/comments/c36ko1/help_with_eap_proxy/)
