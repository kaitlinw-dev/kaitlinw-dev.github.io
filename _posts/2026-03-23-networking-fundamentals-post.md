---
title: "Networking Fundamentals: Understanding TCP/IP, Ports, and Protocols"
date: 2026-03-23
categories: [cybersecurity]
---

This article explores the basics of networking, including TCP/IP, ports, and common protocols, and how they are used in real-world tasks like connecting to systems, analyzing traffic, and understanding how data moves across networks.

<h2>Introduction</h2>

Cybersecurity issues are fundamentally networking issues because nearly all attacks and defenses happen over a network. For cybersecurity professionals, tools like port scanners or packet analyzers become useful with an understanding of what these tools are and how to properly use them. Whether a task requires scanning ports, analyzing traffic, or understanding how attackers move between systems, everything connects back to how devices communicate. 

Despite having a simple understanding of concepts such as ports or IP addresses, when I first started learning cybersecurity, I didn't really understand how these things were all connected in practice - or why they were so important. However, the more I worked through labs or basic exercises, the more I realized just how essential an understanding of networking is. Even tasks such as opening websites or Python scripting - especially for automation - utilize fundamental networking concepts, either explicitly or behind the scenes. In this article, I'm going to break down the basics of networking, specifically TCP/IP, ports, and common protocols, based on what I've been learning so far. All of the content I will present is basic theory and knowledge that I obtained from completing the HackTheBox Introduction to Networking module. I would advise anyone who wants to explore the full extent of this content to check out this module on HackTheBox to learn the theory more deeply than the summaries I will provide below. 

<h2>Tools Used</h2>

- [HackTheBox Introduction to Networking](https://academy.hackthebox.com/course/preview/introduction-to-networking)

<h2>Process</h2>

<h3>IP Addresses</h3>

IP addresses are special number labels that ensure data gets sent to the right place. IP addresses can be thought of as street addresses that people use to find houses, businesses, attractions, etc. On the other hand, MAC addresses are special labels that ensure data gets sent to the right device. MAC addresses can be thought of as the specific person in a house that you are sending mail to or a specific individual room within a large office building. 

Standard IP addresses are in the form of IPv4, which are 32-bit addresses. However, to accomodate for the growth of the internet, IPv6 addresses were created which are 128-bit addresses which allow for many more addresses to be utilized. 

IPv4 addresses consist of 32 bits which are divided into 4 bytes. Each of these 4 bytes is an octet of 8 bits which range in value from 0-255. A way to remember this is that when you take a "bite" of food, you chew it into smaller "bits". The bite you take is always bigger than the bits that it is made of, so 1 byte is bigger than 1 bit. These IP addresses are made of binary bits, meaning 0s and 1s that represent the values 0-255. However, they are often presented in decimal format, which is easier for humans to read and understand and more concise than using long strings of 0s and 1. The IP addresses are then divided into two parts: the host part (assigned by the router) and the network part (assigned by the network administrator). Typically, the beginning bits of the IP address are the network bits and the end bits are the host ones. 

<h3>IP Subnetting</h3>

IP subnetting is the process of dividing an IP address into smaller subnetworks (subnets). This is an important concept, but can be confusing to new learners. In simple terms, IP subnetting can be compared to hard drive partitioning. It must be noted, however, that IP subnetting and hard drive partitioning do not function the same way but that they have a similar high-level purpose of diving one large resource into smaller, more manageable pieces. In hard drive partitioning, the drive is divided into smaller separate pieces that the computer's operating system treats as separate, independent disks. In a similar manner, IP subnetting borrows bits from the host part of the IP address and creates smaller, separate networks where individual devices get assigned. This way, network traffic is managed better and more efficiently so that it doesn't have to travel through the whole network. 

For instance, say you want to visit a friend for lunch at their large office building. If each department of the office was separated into different floors, you would be able to travel directly to the floor of your friend's department to find them. However, if the entire office building had no divisions and every employee was just assigned to a random desk/floor regardless of their department, you might have to travel through the entire building first before you find your friend. Clearly, the first option is much more efficient (and secure), which is the entire benefit of IP subnetting! 

The subnet mask (or netmask) of an IPv4 address is also 32 bits long and it is used to determine which bits of the address are the network bits and which ones are the host bits. If the subnet mask is specified, the host bits are determined using this. The subnet mask of the IP address is specified by the "slash part" that appears at the end of the IP address. For instance in the IP 192.0.0.1/24, it is the /24 part that is in Classless Inter-Domain Routing (CIDR) notation, which specifies the subnet mask in a concise form. The entire subnetmask for this IP would then look like 255.255.255.0. If the subnet mask is not specified, it can be easily obtained by using an IP class table, such as the one below, which is a tool that displays the divisions of IP network blocks and the relevant information regarding those divisions:

| Class	| Network Address | First Address | Last Address | Subnetmask | CIDR | Subnets | IPs |
| ----- | --------------- | ------------- | ------------ | ---------- | ---- | ------- | --- |
| A	| 1.0.0.0 | 1.0.0.1	| 127.255.255.255 | 255.0.0.0 |	/8 | 127 | 16,777,214 + 2 | 
| B	| 128.0.0.0 | 128.0.0.1 | 191.255.255.255 | 255.255.0.0 | /16 | 16,384 | 65,534 + 2 |
| C	| 192.0.0.0	| 192.0.0.1	| 223.255.255.255 | 255.255.255.0 | /24 | 2,097,152 | 254 + 2 |
| D	| 224.0.0.0	| 224.0.0.1	| 239.255.255.255 | Multicast |	Multicast |	Multicast |	Multicast |
| E | 240.0.0.0	| 240.0.0.1	| 255.255.255.255 |	reserved |	reserved |	reserved | reserved |

**Important Note:** In every network, there are two IP addresses that are specially reserved and cannot be used to assign to devices. These addresses are always the first and last ones in the network. The first address is called the network address and is used to identify the network itself by routers. The last address is called the broadcast address and is used to connect all of the devices in the network to each other so that it can send messages to every device at once. 

<h3>IP Subnetting: Guided Examples</h3>

The following examples will demonstrate the steps for how to calculate the corresponding network block information from a given IP address. 

---

**Example 1:** Given IP address: 192.168.1.0/26

Step 1: Calculate the number of host bits: $$32-26=6$$

We have 32 total bits (because it is an IPv4 address), and we are given /26, meaning we have 26 network bits. This means, the rest of the bits are the host bits. In this case, we have 6 host bits. 

Step 2: Calculate the subnet mask

In binary, this subnet mask is: $$11111111.11111111.11111111.11000000$$

Notice how from left to right we fill in the 1s corresponding to the /26 i.e. there are 26 1s. The last bits are 0s which there are 6 of, corresponding to the host bits. 

Next, convert the subnet mask to decimal form: $$255.255.255.192$$

To convert each octet from binary to decimal, you must do the following:

Since octets 1-3 are all the same in this case, I will only demonstrate once:

$$1*2^{7} + 1*2^{6} + 1*2^{5} + 1*2^{4} + 1*2^{3} + 1*2^{2} + 1*2^{1} + 1*2^{0}$$

$$128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 = 255$$

To convert octet 4 the process is the same, but this time the result will be different:

$$1*2^{7} + 1*2^{6} + 0*2^{5} + 0*2^{4} + 0*2^{3} + 0*2^{2} + 0*2^{1} + 0*2^{0}$$

$$128 + 64 + 0 + 0 + 0 + 0 + 0 + 0 = 192$$

When you put them all together you get: $$255.255.255.192$$

Step 3: Calculate the number of hosts per subnet

General formula: $$2^{\text{number of host bits}}-2$$

$$2^{6}-2 = 64-2 = 62$$

This means that we have 62 usable IP addresses in this network.

Step 4: Calculate the size of each subnet: $$256-192=64$$

Step 5: List each subnet

$$192.168.1.0$$<br>$$192.168.1.64$$<br>$$192.168.1.128$$<br>$$192.168.1.192$$

Notice how the last octet is incremented by 64 bits, which is the number we found in step 4.

Step 6: Find the relevant information 

Network address (first address): $$192.168.1.0$$<br>Broadcast address (last address): $$192.168.1.63$$ <br>Usable IP range (the IPs that can be assigned to devices on this subnet): $$192.168.1.1 - 192.168.2.62$$

---

**Example 2:** Given IP address: 10.0.0.0/8

Step 1: Calculate the host bits: $$32-8=24$$

We have 24 host bits

Step 2: Calculate the subnet mask

Binary representation: $$11111111.00000000.00000000.00000000$$

Convert to decimal representation: $$255.0.0.0$$

Step 3: Calculate the number of usable hosts: $$2^{24}-2=16777216-2=16777214$$

We have 16777214 usable hosts in this network. 

**Tip:** In general, the total number of hosts in a network is just: $$2^{\text{number of host bits}}$$

Step 4: Calculate the block size: $$256-255=1$$

Step 5: Calculate the network range

In this case, the next /8 network would start at $$11.0.0.0$$ then $$12.0.0.0$$ and so on.

Step 6: Find the relevant information

Network address: $$10.0.0.0$$<br>Broadcast address: $$10.255.255.255$$<br>Usable IP range: $$10.0.0.1 - 10.255.255.254$$

<h3>HackTheBox Example Walkthroughs</h3>

---

**Question 1:** Find the decimal notation of the subnet mask from the following CIDR: 10.200.20.0/27

32-27=5 so there are 5 host bits

subnet mask: 11111111.11111111.11111111.11100000

128+64+32=210+14=224

**Answer:** <span class="reveal-answer">255.255.255.224</span>

--- 

**Question 2:** Submit the broadcast address of the following CIDR: 10.200.20.0/27

hosts per subnet: 2^5-2 = 32-2=30
size of each subnet: 256-224 = 32 (you subtract the value of the subnet mask in the octet where the network ends - in this case its the last octet, in the /8 example the network bits end in the first octet which is 255) 

blocks:<br>10.200.20.0<br>10.200.20.32<br>10.200.20.64<br>10.200.20.96<br>10.200.20.128<br>10.200.20.160<br>10.200.20.192<br>10.200.20.224

**Tip:** When asked for the broadcast address or network address, the language/wording can be tricky. This means to find the broadcast address of the first specific subnet from the given IP. In this case it means find the broadcast address of 10.200.20.0. If the question had asked about 10.200.20.32/27 instead, then the broadcast address would be different.

**Answer:** <span class="reveal-answer">10.200.20.31</span>

---

**Question 3:** Split the network 10.200.20.0/27 into 4 subnets and submit the network address of the 3rd subnet as the answer.

There are 5 host bits, so the number of hosts is: $$2^5 = 32$$

We need to divide the 32 hosts we know by 4, and we know $$4 = 2^2$$

To determine number of bits to borrow:<br>We want 4 subnets from /27 network<br>Formula: $$2^n >=$$ required subnets so $$2^n >= 4$$ so $$n = 2$$<br>So, we need to borrow 2 bits from host portion

Step 3: new subnet mask<br>Original mask: /27<br>We borrow two bits so the new mask is: $$/27 + 2 = /29$$<br>Host bits left: $$5-2=3$$<br>Total IPs per /29 subnet: $$2^3 = 8$$<br>Usable hosts per /29 subnet: $$8-2 = 6$$


$$32-29=3$$ so we have 3 host bits<br>subnet mask: $$11111111.11111111.11111111.11111000$$<br>$$128+64+32+16+8 = 56+64+128=120+128=248$$<br>Decimal notation: $$255.255.255.248$$

Hosts per subnet: $$2^3 - 2 = 6$$<br>Size of each subnet: $$256-248=8$$<br>Blocks: 10.200.20.0,10.200.20.8,10.200.20.16,10.200.20.24

Original /27 network each range has 32 ips, now each has 8 so: 

| subnet# | network address | broadcast address | usable IPs |
| ------- | --------------- | ----------------- | ---------- |
| 1 | 10.200.20.0 | 10.200.20.7 | 10.200.20.1-6 |
| 2 | 10.200.20.8 | 10.200.20.15 | 10.200.20.9-14 |
| 3 | 10.200.20.16 | 10.200.20.23 | 10.200.20.17-22 |
| 4 | 10.200.20.24 | 10.200.20.31 | 10.200.20.25-30 |

**Answer:** <span class="reveal-answer">10.200.20.16</span>

--- 

**Question 4:** Split the network 10.200.20.0/27 into 4 subnets and submit the broadcast address of the 2nd subnet as the answer.

We can use the previous result for this question.

**Answer:** <span class="reveal-answer">10.200.20.15</span>

<h2>Network Models</h2>

The two main types of network models that exist are the TCP/IP model and the OSI model, which each have different components and purposes, but both serve as the "blueprints" of network communications:

![htb_ositcp_model](/images/htb_ositcp_model.png)

<h3>TCP/IP model</h3>

TCP/IP stands for Transmission Control Protocol/Internet Protocol which details the framework and rules for how data gets transmitted over the Internet. The TCP/IP model serves as the standard set of protocols that devices must follow when sending data over the Internet to ensure smooth communications and allow for easier troubleshooting of issues. This can be thought of like roadway traffic laws, which are a standard set of rules that drivers must follow, ensuring every person on the road knows how to safely and effectively travel to their destinations. After all, it is much easier to prevent accidents and other traffic issues when there are standard driving rules in place, rather than if every individual person on the road had their own set of different rules to follow! 

The TCP/IP model is comprised of four (sometimes five) layers as follows (with 4 being the highest layer and 1 being the lowest):

- 4: Application Layer

    - Responsible for managing data transmission speeds, breaking data streams into smaller segments, establishing communications between applications, etc.

- 3: Transport Layer

    - Responsible for IP routing and managing TCP and UDP sessions for the application layer.

- 2: Internet Layer

    - Responsible for MAC addressing, packet routing and assembly.

- 1: Link Layer

    - Responsible for placing and recieving TCP/IP packets to and from the network medium (physical devices like wires or wireless signals like electromagnetic waves). 

<h3>OSI model</h3>

OSI stands for Open Systems Interconection which details the conceptual framework and rules for how data gets transmitted within a network. The OSI model divides network protocols into layers that build on top of each other to form the entire network communication process. In the forward direction, this can be thought of like a factory line that builds products, where each station on the line has specific tasks that get performed after the previous task is completed until the final product is complete and ready to be shipped. In the reverse direction, this can be thought of like a factory line that unpacks boxes of supplies, where each station takes only the supplies they need until the box is empty. 

The OSI model is comprised of seven layers as follows (with 7 being the highest layer and 1 being the lowest):

- 7: Application Layer

    - Controls input and output of data through user interfaces such as browsers, email, etc.

- 6: Presentation Layer

    - Formats data in a way that is compatible with and readable by the system through operations such as ASCII (character/text) encoding, encryption/decryption, file format conversions, etc. 

- 5: Session Layer

    - Begins, manages and ends the connections between systems for data exchange and communications.

- 4: Transport Layer

    - Facilitates communications by breaking up data streams into smaller segments for easier transportation, managing various ports for data flow, controlling communication speeds, etc. 

- 3: Network Layer

    - Facilitates communications by routing data packets to the correct nodes, using IP addresses to forward information, etc.

- 2: Data-Link Layer

    - Facilitates communications by forwarding data from nodes to specific devices using MAC addresses, ethernet, WiFi, etc. 

- 1: Physical Layer

    - The binary bitstream of the data that is sent to devices through physical mediums such as electrical signals, electromagnetic waves, etc. 


<h2>Challenges & Lessons Learned </h2>

<h3>Types of Networks</h3>

There are many different types of networks and network structures that exist. For a beginner in cybersecurity, it may be useful to become familiar with the most common types of networks and their configurations:

- Wide Area Network (WAN): A large network (commonly known as the Internet itself) that is comprised of many different, smaller networks called LANs. 

- Local Area Network (LAN): A smaller network (i.e. a home network or the network of an office building) that connects individual devices together such as printers, desktops, etc. 

- Wireless Local Area Network (WLAN): The same thing as a LAN, except devices can share data without using cables (think of laptops, tablets, cell phones). 

- Virtual Private Network (VPN): A VPN makes devices appear as if they were connected to a different network than they actually are, without the need to physically travel to another location and connect to that network. 

Networks are typically divided into three categories:

1. Connections 

    - These refer to **how** a device can join a network. Devices can join a network with either physical connections or wireless connections. 

    - Physical connections are things like cables or wires which "plug in" to devices. A commonly known example of this type of connection is an ethernet cable. 

    - Wireless connections are things like WiFi routers, satellites or cell towers which allow devices to join a network without cables or wires. 

2. Nodes/Network Interface Controllers (NICs)

    - These refer to **which** types of devices are connected within a network. There are two main types of nodes in a network which are end nodes and network nodes.

    - End nodes are devices such as printers, laptops, tablets, or phones which are typically the devices that people directly use and interact with. 

    - Network nodes are devices such as gateways, routers, hubs, switches, or firewalls which are typically the devices that direct traffic throughout the network as well as maintaining security and protocols. 

3. Classification

    - This refers to **what** type of structure/configuration a network has. The classification of a network is typically broken into a physical classification and a logical classification. 

    - The physical classification of a network refers to the actual hardware-based arrangement of cables, ports, etc. This can be thought of as where things are. 

    - The logical classification of a network refers to the way that devices are structured/organized to communicate within a network. This is similar to things like file systems, which are ordered in a specific way, regardless of where the computer is physically located. 

<h3>Network Classifications</h3>

There are many types of network classifications, and various classifications can be combined to create hybrid networks as well. Some of the basic network classifications that exist are: 

- Point-to-Point: Two hosts are physically connected to each other with a cable or wire. 

- Bus: Every host is connected through a transmission medium such as a cable, in which one host can send signals and each other host can receive and interpret those signals. This type of network might be familiar to anyone who has experience with implementing AXI protocols (AXI4/AXI4-Lite) using FPGAs (Field Programmable Gate Arrays). 

- Star: Every host is connected to a central network component (such as a router) through a separate link. The central network component directs traffic and information to each host. 

- Ring: Every device is connected with two cables: an ingoing connection and an outgoing connection. In a physical ring classification, information gets forwarded through other devices until it reaches its destination. This is somewhat similar to the classic game of "telephone", except in this case, information keeps getting passed along through the circle (the network) until it reaches the person (device) it is intended for. In a logical ring classification, the devices are not necessarly physically connected in a circle, but the network simulates the circle and acts as if they are. 

- Mesh: Mesh networks have no defined structure. Instead, every network node decides how traffic should be routed in a way that optimizes speed and reliability. In this type of network, if one node fails, traffic gets directed through other nodes instead, ensuring that the information can still travel to its destination without getting lost or having to wait its turn for a long time until it can be passed along. One way to think about mesh networks is like a basketball game, where every person (node) works together to get the ball (the information) into the basket (the destination) in the fastest way possible. If one player gets knocked down or blocked (a node fails), the player (node) who has the ball (the information) will redirect the ball to someone else (a different node) to ensure it gets to the basket (destination) in one way or another. 

- Tree: Tree networks are typically larger versions of star networks that are implemented with some form of hierarchy. For instance, some devices may be connected to a hub that is connected to a server, rather than having every individual device directly connected to the server. 

<h3>MAC Addresses</h3>

Media Access Control (MAC) addresses are 48 bit addresses in hexadecimal format, that represent the physical connection of host such as a network card, ethernet, etc. These addresses have 6 bytes in which the first 3 bytes are the Organization Unique Identifier (OUI) defined by IEEE and the last 3 bytes are the Network Interface Controller (NIC) defined by the manufacturer.

Even though MAC addresses are assigned once by the manufacturer, they can be changed and exploited in several ways such as through MAC spoofing, MAC filtering or MAC flooding. Each of these attacks utilizes device MAC address to gain access to unauthorized information or networks. 

<h2>Next Steps</h2>

- Complete [HackTheBox Nmap Enumeration Lab](https://academy.hackthebox.com/course/preview/network-enumeration-with-nmap)