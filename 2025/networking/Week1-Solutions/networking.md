Deep Digging into Networking for DevOps and daily-use commands

As the title said, networking for DevOps means you do not need to know in-depth about networking like a Networking Engineer. 
But since networking is a critical component of IT infrastructures, I will try to cover important concepts like the OSI model, TCP/IP, the differences between TCP/UDP protocols, IP, Subnetting, CIDR, DNS along with HTTP concepts and some important tips for network management during your DevOps journey.
![image](https://github.com/user-attachments/assets/fd86ef1f-4c47-43a5-9bb9-46870d1e9644)


OSI Model:

![image](https://github.com/user-attachments/assets/c5a893bf-e212-426b-b2e8-a703732b5ec0)

How to remember this OSI model: All People Simply Need Data Processing 

The OSI model is a big chapter, but I am trying to shorten it. It is an open system interconnection that describes how data moves through the network. 
Sound simple? 
As a DevOps engineer, you would mostly need networking concepts in the Virtual Private Cloud where you need to troubleshoot networks because it is a common point for designing and implementing networks.

Software Layer: Application+Presentation+Session Layer

Heart of OSI: Transport Layer

Hardware Layer: Network+DataLink+Physical Layer

Layer 1: Physical: First and bottom layer:
· It converts data into bits and transmits them over the physical network.
· This layer includes various communications like wi-fi and Bluetooth.
· Some other protocols like ethernet, USB, and HDMI as well.

Layer 2: Data Link Layer:
· This layer takes data in the form of electric signals like frames in the local network only
· It uses physical addresses MAC to identify devices in the same network segment.
· Usually copper wire or fiber optic cable is used.

Layer 3: Network:
· It maintains end-to-end communication between two hosts of different networks.
· It provides routing service and packet data transfer across different networks using routing.
· Monitoring networks and flow of data.
· Protocols used in this layer are IP/ICMP/IGMP.
· Medium used here is routers and switches.

Layer 4: Transport:
· This layer provides data delivery end-to-end between applications and hosts of different networks.
· Takes data segments from the session layer, breaks them into smaller packets, and transmits them over the network.
· Medium used here is fiber optic or wireless communications.
· Protocols used here are TCP/UDP.

Layer 5: Session:
· It maintains, manage applications sessions between devices and keep tracking data exchanges.
· It synchronizes, encrypts, and recovers session data.
· It interacts with the presentation and transport layer

Later 6: Presentation:
· It ensures data exchange regardless of data format.
· It encrypts, decrypts, compresses, and decompresses data and securely transmits data on the unsecured network.

Layer 7: Application
· This layer allows users to interact with the applications to exchange information with other devices.
· Applications like email, web browsing, file transfer, and remote access.
· Protocols used here are HTTP, FTP, and SMTP telnet.

Now we need to understand how each layer communicates with each other in real-life scenarios:
![image](https://github.com/user-attachments/assets/d7d09234-0fbe-45a3-9cae-417f6d7e9c16)

As we can see in the picture above:

Layer7-Application->Using HTTP protocol, this layer sends the request to the webserver then, the user can see the webpage after the verification process happens between them.

Layer6-Presentation-> When a user sends an email for example, this layer encrypts data to prevent tampering, compresses it to make sure it delivers fast, and translates it into a suitable format to read for users.

Layer5-Session-> When the user plays a game online for example, this layer creates, maintains, synchronizes,s and stores user data until the game stops.

Layer4-Transport-> VPN for example. when the user sends large files to another server using a VPN, this layer ensures speed and connection reliability, making data segments for smooth transmission using TCP/UDP protocol.

Layer3-Network-> This layer makes communication between two different networks using routing tables to find the best routes.

Layer2-DataLink-> Ethernet switches use MAC addresses for inter-network communications and frame the data to travel to the physical devices.

Layer1-Physical-> This works for actual physical devices for communication by transmitting data as signals through wired or wireless. eg. Bluetooth

Now how TCP/IP protocols are associated with devOps?

It's simple, two sets of protocols provide connection for transmitting data between devices.
TCP/IP is the most widely used networking protocol suite in DevOps networking. It provides a reliable, connection-oriented communication model for transmitting data between devices.

TCP provides reliable and ordered data delivery
IP provides routing and addressing capabilities.
TCP/IP consisted of 4 OSI layers:
Network, Internet, Transport and Application.

![image](https://github.com/user-attachments/assets/47eea0de-998e-48f0-85ef-b157d8fcd12e)


TCP vs UDP:
· TCP connection-oriented, reliable guaranteed delivery, acknowledgment available.
UDP connectionless protocol, transmits data without guarantee, packet loss such as video streaming and online gaming.
· TCP Reliable but slower
UDP is faster but not reliable

IP Subnetting and CIDR:

Subnetting means dividing a larger network into a smaller one or subnets. Subnets are created with unique network addresses and configure them to work as a single network.
now why devops need subnetting?
allocating IP addresses more efficiently so that less wastage of addresses.
it helps isolate networks' sensitive resources and limits access.
dividing smaller network provides better network performance, less traffic congestion.

An IP address is a 32-bit number divided into 4*8 bit sections called octets.

![image](https://github.com/user-attachments/assets/dbe5ea15-7427-4d43-89e2-04d1ded02f33)


Every IP contains a subnet mask, network ID, and host ID part. For example, given an IP address of 192.168.12.20 with the subnet mask of 255.255.255.0, 192.168.12 represents a network address and .20 represents a host address. The concept of a netmask leads us to the idea of classful addressing, which divides the 32-bit IP address into 5 sub-classes.
In classfull addressing, IP addresses have 3 network prefixes: 
8-bit →ClassA →(8-bit networkID, 24-bit hostID)=over 16million addresses
16-bit →ClassB →(8-bits network/hostID)=65,535 addresses
32-bit →ClassC →(24-bit networkID, 8-bit hostID)=smallest 254 addresses

Problems:

what would you do when you 1000 need addresses, it is more than 254 but less than 65,535 right?

Solutions:

Class B? No you need only 1000 addresses but classB will give you 65k addresses and you are occupying only 1000 and rest of the addresses are a big waste.

So what is the best way?

CIDR! Yes, cidr is the solution here which will create a subnet mask of different sizes within a network.
CIDR is denoted by a slash followed by a number that determines the number of IP addresses.
For example, the IP address 172.16.3.0/24 or 192.16.4.0/24 will create 256 hosts. An IP address range 172.16.0.0–172.16.255.255 contains 65k addresses. so the CIDR for any picked-up IP 172.16.4.0/24 will create 256 IP addresses (32–24=2*8=256). /27 will create 32 addresses (32–27=5*2=32).


Commonly used Networking commands for DevOps daily life:


Ping: Tests the reachability of a host on a network. eg: pint google.com

traceroutes(or tracert on windows). Displays the route packets take to a network host. eg: traceroute google.com

ifconfig/ipconfig: Displays or configures network interfaces. eg: ipconfig and ip addr show.

netstat: Displays network connections, routing tables, interface statistics, etc. eg: netstat -tuln

curl: it stands for client URL. it fetches data from the web or API and text-based documents. eg: curl -o  http://reqres.in/api -o will create a output.

wget: It is used to download files from the web. esp. .tar, .zip file for download purposes. eg: 

nslookup: Queries the Domain Name System (DNS) to obtain a domain name or IP address mapping. eg: nslookup google.com

dig: Another DNS lookup tool that provides more detailed information than nslookup. eg: dig google.com

ssh/telnet: connect server over the internet. telnet is a text-based command non-encrypted and ssh is secured. 

scp: securely copies files between two hosts in a network. eg: scp file.txt ec2-user@172.99.22.23:/home/devops.


Conclusion


We have explored topics ranging from the fundamentals to advanced level in DevOps networking.

Let us summarize the key takeaways from this blog:

The OSI model breaks down network communication into seven distinct layers.

TCP/IP is a widely used networking protocol stack today and differs from the OSI model in several ways.

IP subnetting and CIDR are critical concepts in network design and are used to divide a network into smaller, more manageable subnets.

Routing forward packets to different networks.

DNS is the system used to translate domain names into IP addresses.

The HTTP protocol is used for transmitting data over the World Wide Web and is critical for building modern web applications.

Network troubleshooting tools can help DevOps engineers diagnose and resolve issues quickly.
