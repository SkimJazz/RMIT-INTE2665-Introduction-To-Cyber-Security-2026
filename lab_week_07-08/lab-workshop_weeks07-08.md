# RMIT - INTE2665 Intro to Cyber Security Lab Workshops Weeks 7-8

## Packet Analysis with Wireshark

Run Wireshark

In the Kali Linux VM, run below command to start Wireshark.

`wireshark`

You can also execute it from Applications.

Applications >> 09 - Sniffing & Spoofing >> wireshark

Navigate to Applications at the top left corner, click 09 - Sniffing & Spoofing, and then click Wireshark.
You will see below user interface.

ref: img inserted here page

### Task-1.2: Capturing a network packet

To analyze the network functionalities, you need to capture packets first. First, you need to choose a network interface of your computer that should be used to capture packets. As you are running Wireshark on the Kali Linux VM, choose interface as below.

- Choose eth0 (if you are using only one network interface - Bridge Adaptor) or
- Choose eth1 (if you are using two network adaptors, where first network adaptor is NAT and 2nd is Host Only adaptor).

In most cases, you will have only eth0 option available. Therefore, select this one to proceed.
Once you choose an interface, start the packet capturing process by selecting the start option from the menu bar of the Wireshark:

- Select **Capture** from the menu bar
- Then, select **Start** from the drop-down menu.

Ref: img inserted page 2

Wireshark will start capturing all the packets on the selected interface automatically.

You will see the following screen after capturing some packets.

ref: img inserted here page 3

### Task-1.3: Understanding major components of Wireshark interface

ref: img inserted here page 4

The Wireshark interface has below major components:

- **1-Menu** is located at the top of the window. You will mainly use the File and Capture menus. The File menu allows you to save captured packet data or open a file containing previously captured packet data and exit the Wireshark application. The Capture menu allows you to start or stop packet capture.
- **2-Toolbar**. This is a quick access toolbar providing easy-to-use buttons for the most common functions of the main menu. Most of these buttons become active only after you’ve selected an interface to monitor.
- **3-Display filter** You can apply a display filter to filter the information displayed in the packet-listing window in the packet display filter field. You can find more details of filtering syntax in the following link. https://www.wireshark.org/docs/man-pages/wireshark-filter.html
- **4-The packet-listing window** displays a one-line summary of each captured packet, including a packet number assigned by Wireshark, the time at which the packet was captured, the source and destination IP addresses of the packet, the protocol type, and protocol-specific information contained in the packet.
- **5-The packet-header details window** provides details about the packet selected (highlighted) in the packet listing window. These details include information about the Ethernet frame and IP datagram contained in this packet.
- **6-The packet-contents window** displays the contents of the captured frame, in both ASCII and hexadecimal format.
- **7-Statusbar** contains informational messages.

## Part-2: Wireshark configuration

Before capturing the network traffic some configuration is needed.

### Task-2-1: Manage Interfaces

First of all, remove unnecessary interfaces from Input tab. Only “eth0” and “any” are needed. Go the Wireshark menu: Select Capture and then select Options.

You will see the following interface:
Click the Manage Interfaces button as shown in the above screenshot. Only select “eth0” and “any” and deselect the remaining. Click OK to exit.

Now only two interfaces will be shown.

### Task-2-2: Managing Name Resolution

Under the Capture Options window, Select Options Tab. On the right under Name Resolution, select Resolve Network names and Resolve transport names. After this settings DNS address will be shown in Source and Destination columns on the captures traffic screen.

### Task-2-3: IP Address

Find your computer’s IP address. Open a Terminal, type hostname -I command, and press Enter. Take note of your IP address.
Note: It should be different in your case to what is shown here.

### Task-3.1: Capture Network traffic

In this activity 192.168.4.97 is the IP address of the VM. Note down the IP address of your VM.
Now the wireshark is ready to start capturing the network traffic.
Click Capture and then click Start button from command toolbar.
Access https://www.yahoo.com url from command terminal with wget command as follows:
Once above command completes, wait about 5 seconds, then stop capturing traffic.

### Task 3-2: Saving and Opening Capture Files

• Saving: File -> Save As... (.pcapng or .pcap format)
• Opening: File -> Open
3.1: Packet Filtering
Filter protocols
Stop previous capture and start new capture. Access some sample websites from command terminal with wget command.
e.g., www.yahoo.com, www.example.com, www.yourtube.com and neverssl.com
Stop capture and filter packets on protocols e.g., dns and http protocols one by one.
Filter port https port
Things to do.
See filters from https://www.wireshark.org/docs/man-pages/wireshark-filter.html and apply some of the filters on the captured data.
Congratulations!
You have now completed the capture and analysis network traffic using WIRESHARK.
You can find more details of filtering syntax in the following link:
https://www.wireshark.org/docs/man-pages/wireshark-filter.html
More exercises to experiment with Wireshark
You can use ping utility to test whether a host is alive or not and use Wireshark to analyse the ICMP packets.
Ping utility:
https://en.wikipedia.org/wiki/Ping_(networking_utility)
ICMP:
https://en.wikipedia.org/wiki/Internet_Control_Message_Protocol
