      Basic Linux Commands

When it comes to hacking, knowledge is power. The more knowledge you have about a target system or network, the more options you have available. This makes it imperative that proper enumeration is carried out before any exploitation attempts are made.

Say we have been given an IP (or multiple IP addresses) to perform a security audit on. Before we do anything else, we need to get an idea of the “landscape” we are attacking. What this means is that we need to establish which services are running on the targets. For example, perhaps one of them is running a webserver, and another is acting as a Windows Active Directory Domain Controller. The first stage in establishing this “map” of the landscape is something called port scanning. When a computer runs a network service, it opens a networking construct called a “port” to receive the connection.  Ports are necessary for making multiple network requests or having multiple services available. For example, when you load several webpages at once in a web browser, the program must have some way of determining which tab is loading which web page. This is done by establishing connections to the remote webservers using different ports on your local machine. Equally, if you want a server to be able to run more than one service (for example, perhaps you want your webserver to run both HTTP and HTTPS versions of the site), then you need some way to direct the traffic to the appropriate service. Once again, ports are the solution to this. Network connections are made between two ports – an open port listening on the server and a randomly selected port on your own computer. For example, when you connect to a web page, your computer may open port 49534 to connect to the server’s port 443.

As in the previous example, the diagram shows what happens when you connect to numerous websites at the same time. Your computer opens up a different, high-numbered port (at random), which it uses for all its communications with the remote server.
Every computer has a total of 65535 available ports; however, many of these are registered as standard ports. For example, a HTTP Webservice can nearly always be found on port 80 of the server. A HTTPS Webservice can be found on port 443. Windows NETBIOS can be found on port 139 and SMB can be found on port 445. It is important to note; however, that especially in a CTF setting, it is not unheard of for even these standard ports to be altered, making it even more imperative that we perform appropriate enumeration on the target.
If we do not know which of these ports a server has open, then we do not have a hope of successfully attacking the target; thus, it is crucial that we begin any attack with a port scan. This can be accomplished in a variety of ways – usually using a tool called nmap, which is the focus of this room. Nmap can be used to perform many different kinds of port scan – the most common of these will be introduced in upcoming tasks; however, the basic theory is this: nmap will connect to each port of the target in turn. Depending on how the port responds, it can be determined as being open, closed, or filtered (usually by a firewall). Once we know which ports are open, we can then look at enumerating which services are running on each port – either manually, or more commonly using nmap.
So, why nmap? The short answer is that it's currently the industry standard for a reason: no other port scanning tool comes close to matching its functionality (although some newcomers are now matching it for speed). It is an extremely powerful tool – made even more powerful by its scripting engine which can be used to scan for vulnerabilities, and in some cases even perform the exploit directly! Once again, this will be covered more in upcoming tasks.
For now, it is important that you understand: what port scanning is; why it is necessary; and that nmap is the tool of choice for any kind of initial enumeration.


Tools:

Nmap: Open source tool for network discovery and security auditing. The program can be used to find live hosts on a network, perform port scanning, ping sweeps, OS detection, and version detection. Our first objective is to obtain a "map" of the network structure -- or, in other words, we want to see which IP addresses contain active hosts, and which do not. Nmap is used to discover hosts and services on a computer network by sending packets and analyzing the responses. Nmap provides a number of features for probing computer networks, including host discovery and service and operating system detection.











Commonly hacked Ports:

Common ports, such as TCP port 80 (HTTP), may be locked down — but other ports may get overlooked and be vulnerable to hackers. In your security tests, be sure to check these commonly hacked TCP and UDP ports:
TCP port 21 — FTP (File Transfer Protocol) 
TCP port 22 — SSH (Secure Shell) 
TCP port 23 — Telnet 
TCP port 25 — SMTP (Simple Mail Transfer Protocol) 
TCP and UDP port 53 — DNS (Domain Name System) 
TCP port 443 — HTTP (Hypertext Transport Protocol) and HTTPS (HTTP over SSL) 
TCP port 110 — POP3 (Post Office Protocol version 3) 
TCP and UDP port 135 — Windows RPC 
TCP and UDP ports 137–139 — Windows NetBIOS over TCP/IP 
TCP port 1433 and UDP port 1434 — Microsoft SQL Server 
Part of Hacking For Dummies Cheat Sheet


Common Directories:

/etc: This root directory is one of the most important root
        directories on your system. The etc folder (short for etcetera)
        is a commonplace location to store system files that are 
        used by your operating system.

/var: This folder stores data that is frequently accessed or written
         by services or applications running on the system. For
         example, log files from running services and applications
         are written here (/var/log), or other data that is not
         necessarily associated with a specific user (i.e., databases
         and the like).

/root: Unlike the /home directory, the /root folder is actually the
          home for the "root" system user. There isn't anything more
          to this folder other than just understanding that this is the
          home directory for the "root" user. But, it is worth a
          mention as the logical presumption is that this user would
          have their data in a directory such as "/home/root" by
          default.


/tmp: This is a unique root directory found on a Linux install.
          Short for "temporary", the /tmp directory is volatile and is
          used to store data that is only needed to be accessed
          once or twice. Similar to the memory on your computer,
          once the computer is restarted, the contents of this folder
          are cleared out.

/var/log directory: these files and folders contain logging
         information for applications and services running on your
         system. The Operating System  (OS) has become pretty
         good at automatically managing these logs in a process
         that is known as “rotating".




Symbols and Operators:

&: This operator allows you to run commands in the background               
    of your terminal.

&&: This operator allows you to combine multiple commands  
       together in one line of your terminal.

>: (Less Than) This operator is a redirector - meaning that we can  
    output from a command (such as using cat to output a file)
     and direct it elsewhere.

>>: (Less than) This operator does the same function of 
      the > operator but  appends the output rather than replacing 
      (meaning nothing is overwritten).    
  



|: (ps -A | more) Piping is a way to send the output of one
   command to another command as input. The
   command more allows you to show only one page/screen’s 
   worth of information, and allows you to then hit enter to scroll
   through data one line at a time.

<: (Greater than) Write it to a file.

<<: (Greater than)  Append or add to that file.

||: or operator (acts like else in programming).



Flags and Switches: (used to advance commands)


-a: to get all hidden files.

—help: This option will list the possible options that the
      command accepts, provide a brief description and example
      of how to use it. Example of this is:  ls —help.

-f: use to force close or force a command.




-l: Shows permissions. Example is: ls -l or ls -la.

The diagram below is a great representation of how these permissions can be translated.


OSI Model:


7. Application: The application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received.

6. Presentation: This layer acts as a translator for data to and from the application layer (layer 7). Security features such as data encryption (like HTTPS when visiting a secure site) occur at this layer.

5. Session: The session layer (layer 5) synchronises the two computers to ensure that they are on the same page before data is sent and received. Once these checks are in place, the session layer will begin to divide up the data sent into smaller chunks of data and begin to send these chunks (packets) one at a time.

4. Transport: Layer 4 of the OSI model plays a vital part in transmitting data across a network and can be a little bit difficult to grasp. When data is sent between devices, it follows one of two different protocols that are decided based upon several factors:
TCP
UDP

3. Network: The third layer of the OSI model (network layer) is where the magic of routing & re-assembly of data takes place (from these small chunks to the larger chunk). Firstly, routing simply determines the most optimal path in which these chunks of data should be sent.

2. Data Link: he data link layer focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint. Inside every network-enabled computer is a Network Interface Card (NIC) which comes with a unique MAC address to identify it. Additionally, it's also the job of the data link layer to present the data in a format suitable for transmission.

1. Physical: This layer is one of the easiest layers to grasp. Put simply, this layer references the physical components of the hardware used in networking and is the lowest layer that you will find. Devices use electrical signals to transfer data between each other in a binary numbering system (1's and 0's).
For example, ethernet cables connecting devices.



Encapsulation:

As the data is passed down each layer of the model, more information containing details specific to the layer in question is added on to the start of the transmission. As an example, the header added by the Network Layer would include things like the source and destination IP addresses, and the header added by the Transport Layer would include (amongst other things) information specific to the protocol being used. The data link layer also adds a piece on at the end of the transmission, which is used to verify that the data has not been corrupted on transmission; this also has the added bonus of increased security, as the data can't be intercepted and tampered with without breaking the trailer. This whole process is referred to as encapsulation; the process by which data can be sent from one computer to another.

Notice that the encapsulated data is given a different name at different steps of the process. In layers 7,6 and 5, the data is simply referred to as data. In the transport layer the encapsulated data is referred to as a segment or a datagram (depending on whether TCP or UDP has been selected as a transmission protocol). At the Network Layer, the data is referred to as a packet. When the packet gets passed down to the Data Link layer it becomes a frame, and by the time it's transmitted across a network the frame has been broken down into bits.
When the message is received by the second computer, it reverses the process -- starting at the physical layer and working up until it reaches the application layer, stripping off the added information as it goes. This is referred to as de-encapsulation. As such you can think of the layers of the OSI model as existing inside every computer with network capabilities. Whilst it's not actually as clear cut in practice, computers all follow the same process of encapsulation to send data and de-encapsulation upon receiving it.
The processes of encapsulation and de-encapsulation are very important -- not least because of their practical use, but also because they give us a standardised method for sending data. This means that all transmissions will consistently follow the same methodology, allowing any network enabled device to send a request to any other reachable device and be sure that it will be understood -- regardless of whether they are from the same manufacturer; use the same operating system; or any other factors.

TCP/IP Model:

The two models match up something like this:

The processes of encapsulation and de-encapsulation work in exactly the same way with the TCP/IP model as they do with the OSI model. At each layer of the TCP/IP model a header is added during encapsulation, and removed during de-encapsulation.
TCP (or Transmission Control Protocol for short) is another one of these rules used in networking.
This protocol is very similar to the OSI model that we have previously discussed in room three of this module so far. The TCP/IP protocol consists of four layers and is arguably just a summarised version of the OSI model. These layers are:
Application
Transport
Internet
Network Interface

TCP: (Transmission Control Protocol) Is a connection-based protocol. In other words, before you send any data via TCP, you must first form a stable connection between the two computers. The process of forming this connection is called the three-way handshake. Bite-sized pieces (segments).

TCP/IP: TCP/IP model was introduced by the American DoD in 1982 to provide a standard -- something for all of the different manufacturers to follow.

UDP: User Datagram Protocol. Bite-sized pieces (datagrams).
Useful in video streaming and small pieces of data. For example, protocols used for discovering devices (ARP and DHCP).

As mentioned earlier, TCP is a connection-based protocol. In other words, before you send any data via TCP, you must first form a stable connection between the two computers. The process of forming this connection is called the three-way handshake.
When you attempt to make a connection, your computer first sends a special request to the remote server indicating that it wants to initialise a connection. This request contains something called a SYN (short for synchronise) bit, which essentially makes first contact in starting the connection process. The server will then respond with a packet containing the SYN bit, as well as another "acknowledgement" bit, called ACK. Finally, your computer will send a packet that contains the ACK bit by itself, confirming that the connection has been setup successfully. With the three-way handshake successfully completed, data can be reliably transmitted between the two computers. Any data that is lost or corrupted on transmission is re-sent, thus leading to a connection which appears to be lossless.

Very similar to how the OSI model works, information is added to each layer of the TCP model as the piece of data (or packet) traverses it. As you may recall, this process is known as encapsulation - where the reverse of this process is decapsulation.
 
One defining feature of TCP is that it is connection-based, which means that TCP must establish a connection between both a client and a device acting as a server before data is sent.
 
Because of this, TCP guarantees that any data sent will be received on the other end. This process is named the Three-way handshake, which is something we'll come on to discuss shortly. A table comparing the advantages and disadvantages of TCP is located below:
 

 
TCP packets contain various sections of information known as headers that are added from encapsulation. Let's explain some of the crucial headers in the table below:
 

 Next, we'll come on to discuss the Three-way handshake - the term given for the process used to establish a connection between two devices. The Three-way handshake communicates using a few special messages - the table below highlights the main ones:
 

The diagram below shows a normal Three-way handshake process between Alice and Bob. In real life, this would be between two devices.

 
Any sent data is given a random number sequence and is reconstructed using this number sequence and incrementing by 1. Both computers must agree on the same number sequence for data to be sent in the correct order. This order is agreed upon during three steps:
SYN - Client: Here's my Initial Number Sequence (ISN) to SYNchronise with (0)
SYN/ACK - Server: Here's my Initial Number Sequence (ISN) to SYNchronise with (5,000), and I ACKnowledge your initial number sequence (0)
ACK - Client: I ACKnowledge your Initial Number Sequence (ISN) of (5,000), here is some data that is my ISN+1 (5,000 + 1)

TCP Closing a Connection:

Let's quickly explain the process behind TCP closing a connection. First, TCP will close a connection once a device has determined that the other device has successfully received all of the data.
Because TCP reserves system resources on a device, it is best practice to close TCP connections as soon as possible.
To initiate the closure of a TCP connection, the device will send a "FIN" packet to the other device. Of course, with TCP, the other device will also have to acknowledge this packet.
Let's show this process using Alice and Bob as we have previously.
 
In the illustration, we can see that Alice has sent Bob a "FIN" packet. Because Bob received this, he will let Alice know that he received it and that he also wants to close the connection (using FIN). Alice has heard Bob loud and clear and will let Bob know that she acknowledges this.



UDP/IP:

The User Datagram Protocol (UDP) is another protocol that is used to communicate data between devices.
 
Unlike its brother TCP, UDP is a stateless protocol that doesn't require a constant connection between the two devices for data to be sent. For example, the Three-way handshake does not occur, nor is there any synchronisation between the two devices.
 
Recall some of the comparisons made about these two protocols in Room 3: "OSI Model". Namely, UDP is used in situations where applications can tolerate data being lost (such as video streaming or voice chat) or in scenarios where an unstable connection is not the end-all. A table comparing the advantages and disadvantages of UDP is located below:
 

 As mentioned, no process takes place in setting up a connection between two devices. Meaning that there is no regard for whether or not data is received, and there are no safeguards such as those offered by TCP, such as data integrity.
 
UDP packets are much simpler than TCP packets and have fewer headers. However, both protocols share some standard headers, which are what is annotated in the table below:
 

Next, we'll come on to discuss how the process of a connection via UDP differs from that of something such as TCP.  We should recall that UDP is stateless. No acknowledgement is sent during a connection.
 
The diagram below shows a normal UDP connection between Alice and Bob. In real life, this would be between two devices.




Putting it all together: Learn how all the individual components of the web work together to bring you access to your favorite web sites.

From the previous modules, you'll have learned that quite a lot of things go on behind the scenes when you request a webpage in your browser. 
To summarise, when you request a website, your computer needs to know the server's IP address it needs to talk to; for this, it uses DNS. Your computer then talks to the web server using a special set of commands called the HTTP protocol; the webserver then returns HTML, JavaScript, CSS, Images, etc., which your browser then uses to correctly format and display the website to you.

Commands:


man: (manual) Example is: man ls. To get that commands manual
         which list switches and flags.

ping: usually used as a simple way to verify that a computer can
         communicate with another computer or network device.
         ping <target>.

traceroute: Traceroute can be used to map the path your request takes as it heads to the target machine. traceroute <destination>

echo: Output any text that we provide, to the console or terminal.

whoami: Find out what user were currently logged in as!

dig: allows us to manually query recursive DNS servers of our choice for information about domains:
dig <domain> @<dns-server-ip>
It is a very useful tool for network troubleshooting.

whois: to get a list of available information about the domain registration: whois <domain>

ls: Listing.

cd: Change directory.

cat: Concatenate. Print out contents on a file.

less: utility used to read contents of a text file one page per time. 

pwd: Print working directory.

find: Used look into directories and files.

grep: Command that allows us to search the contents of files for
         specific values that we are looking for. Used to search a  
         given file for patterns specified by the user.
         


tr: Command is used for translating or deleting characters.
cut: Is used to extract sections from each line of input - usually        
       from a file.

SSH Protocol:  allows us to remotely execute commands on another device
        remotely. Any data sent between the devices is encrypted
        when it is sent over a network such as the Internet.
        (ssh username@machine_IP)

touch: Create a file.

mkdir:  Create a directory.

cp: copy file or folder.

mv: Move file or folder.

rm: Removes file or folder.

file: determine the type of a file.


su or sudo: (sudo) Elevate user permissions. Substitute user
                   identity. Switching between users on a Linux install.

more: (more /etc/services) You can also use more in a stand-
          alone fashion as well. Let’s use more to read the large /etc/
          services file, which contains common port to service
          mappings.

history: Prints out history. 

apt-get-update: update.

apt-get-install: install.




ifconfig: (ipconfig for windows) It shows basic network details
               such as IP addresses, broadcast address, mac address, 
               and much more.

iwconfig: It is similar to the ifconfig command.nIt is more focused 
               on only wireless network interfaces.


netstat: Delivers basic statistics on all network activities and
             informs users on which ports and addresses the
             corresponding connections (TCP, UDP) are running and
             which ports are open for tasks.

route: Fetches the routing table. It basically tells where all
          network is actually routed.



wget: This command allows us to download files from the web
          via HTTP - as is you were accessing the file in your
          browser.  Example if we wanted to download a file named
          “my file.txt” onto my machine, assuming I knew the web
          address it would look something like this:
          wget https://assets.tryhackme.com/additional/linux-
          fundamentals/part3/myfile.txt

ps: command to provide a list of the running processes as our
      user’s session that is running it, how much usage time of the
      CPU it is using, and the name of the actual program or
      command that is being executed.

ps -A: ability to see running processes.



ps aux: to see the processes run by other users and those that
 don’t run from a session, we add the aux to the ps command.


Below are some of the signals that we can send to a process when it is killed:
SIGTERM - Kill the process, but allow it to do some cleanup tasks beforehand
 SIGKILL - Kill the process - doesn't do any cleanup after the fact
SIGSTOP - Stop/suspend a process

ctrl + z: Will run a processes in the background.

fg: Will bring the processes back to the foreground.


top: top command gives real time statistics about the processes
       running on your system instead of a one-time view.


kill:  kill a process by using the kill command along with the
       processes PID number. Example kill 1337.

 




Cyber Security Glossary:

Enumeration: a process which establishes an active connection to the target hosts to discover potential attack vectors in the system, and the same can be used for further exploitation of the system." - Infosec Institute. It is a critical phase when considering how to enumerate and exploit a remote machine - as the information you will use to inform your attacks will come from this stage.

Port Forwarding: Port forwarding is an essential component in connecting applications and services to the Internet. Without port forwarding, applications and services such as web servers are only available to devices within the same direct network (known as intranet). Port forwarding is configured at the router of a network.

URL: Uniform Resource Locator.


NFS: Network File System.

SMTP: Simple Mail Transfer Protocol.

SQL: Structured Query Language.

MAC: (Media Access Control) Inside every network enabled computer is a Network Interface Card (NIC) which comes with a unique MAC (Media Access Control) address to identify it.


LAN: (Local Area Network) Topology.
Data Link Layer: Presents data in suitable format for transmission.

NIC: (Network Interface Card) Inside every network enabled computer is a Network Interface Card (NIC) which comes with a unique MAC (Media Access Control) address to identify it.

RFC: request for Comments is a publication from the Internet Society (ISOC) and it’s associated bodies, most prominently the Internet Engineering Task Force (IETF), the principle technical development and standards-setting bodies for the internet.


CVE: Common Vulnerabilities and Exposures, is a list of publicly disclosed computer security flaws.


ICMP: Internet Control Message Protocol.

SYN: Synchronize. SYN and ACK make up the three way handshake needed to make a connection between two devices.

ACK: Acknowledgement.


IP: (Internet Protocol) IPv4 and IPv6. The IP address uniquely identifies each internet connected device, like a web server or your computer. These are formed of 4 groups of numbers, each 0-255 (x.x.x.x) and called an octet. An example is 100.70.172.11.

IPv4:

IPv6:

ARP: (Address Resolution Protocol) used to find IP to MAC
       address mappings (or a hardware address) to an IP address.

DHCP: Dynamic Configuration Protocol. DHCP Server is a network server that automatically provides and assigns IP addresses, default gateways and other network parameters to client devices.

CIDR notation: Is a compact representation of an IP address and its associated network mask.

TTL: Time to live (TTL) refers to the amount of time or “hops” that a packet is set to exist inside a network before being discarded by a router.


Switch: Used to connect computers and servers into a single network. The switch performs the function of a controller and allows the devices within a network to communicate with each other.

TOS: Type of Service.

NSE: Nmap Scripting Engine.

SNMP: Simple Network Management Protocol.

Firewall:

IDS: Intrusion Detection System.

GUI: Graphic User interface.


WAF: Web Application Firewall.


RDP: Remote Desktop Protocol.


UAC: User Account Control.


NTFS: New Technology File System (Windows10). The file system used in modern versions of Windows is the New Technology File System or simply NTFS. NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file. This function is not possible with FAT16/FAT32.

NFS: Network File System and allows a system to share directories and files with others over a network. By using NFS, users and programs can access files on remote systems almost as if they were local files.

FAT16/FAT32: Before NTFS, there was FAT16/FAT32 (File Allocation Table) and HPFS (High Performance File System).

OSINT: (Open Source Intelligence)  is the practice of collecting information from published or otherwise publicly available sources. OSINT is vital to understand incident response in today's cyber world. It is a combination of any proper threat intelligence operation, providing useful information about a particular threat or risk that you need to be aware of before attackers do.

DNS: Is a TCP/IP protocol (Domain Name System) server. 
DNS is like a giant phone book that takes a URL (Like https://tryhackme.com/) and turns it into an IP address. This means that people don’t have to remember IP addresses for their favorite websites.

ISPs: Internet Service Providers.

TLD: Top Level Domain server.

OSPF: Open Shortest Path First.

RIP: Routing Information Protocol.

OSI: (OSI Model) Open Systems interconnection. Later the OSI model was also introduced by the International Organization for Standardization (ISO); however, it's mainly used as a more comprehensive guide for learning, as the TCP/IP model is still the standard upon which modern networking is based.


Hops: 

Gateway:


Port: is a port number used in a network on a switch.

DHCP: (Dynamic Host Configuration Protocol) server. Used for requesting a IP address if you don’t already have one.
URL: (Uniform Resource Locator) A URL is nothing more than the address of a given unique resource on the Web. In theory, each valid URL points to a unique resource.

HTTP: (Hypertext Transfer Protocol) The communications protocol used to connect to Web servers on the Internet or on a local network (intranet). It runs on port 80.

HTTPS: (Runs on port 443) For most websites now, these requests will use HTTPS. HTTPS is a secure (encrypted) version of HTTP, it works in more or less the same way. This uses TLS 1.3 (normally) encryption in order to communicate without.


TLS:

SSL: (Secure Sockets Layer) is a cryptographic protocol designed to provide communications security over a computer network.

SIG: Standardized Information Gathering.

SIEM: Security Information and Event Management.





SSH: (Secure Shell) allows us to remotely execute commands on another device remotely.Simply is a protocol between devices in an encrypted form. 
PAM: (Linux) pluggable Authentication Modules. PAM is a suite of libraries that allows a Linux system administrator to configure methods to authenticate users.  

VPN: Virtual Private Network.

SMB: Server Message Block Protocol. Is a client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network. [source]
The SMB protocol is known as a response-request protocol, meaning that it transmits multiple messages between the client and server to establish a connection. Clients connect to servers using TCP/IP (actually NetBIOS over TCP/IP as specified in RFC1001 and RFC1002), NetBEUI or IPX/SPX.


FTP: File Transfer Protocol (FTP) is, as the name suggests , a protocol used to allow remote transfer of files over a network. It uses a client-server model to do this, and- as we'll come on to later- relays commands and data in a very efficient way.
A typical FTP session operates using two channels:
a command (sometimes called the control) channel
a data channel.

The FTP server may support either Active or Passive connections, or both. 
In an Active FTP connection, the client opens a port and listens. The server is required to actively connect to it. 
In a Passive FTP connection, the server opens a port and listens (passively) and the client connects to it. 

NFS: NFS stands for "Network File System" and allows a system to share directories and files with others over a network. By using NFS, users and programs can access files on remote systems almost as if they were local files. It does this by mounting all, or a portion of a file system on a server. The portion of the file system that is mounted can be accessed by clients with whatever privileges are assigned to each file.



Telnet: Telnet is an application protocol which allows you, with the use of a telnet client, to connect to and execute commands on a remote machine that's hosting a telnet server. The telnet client will establish a connection with the server. The client will then become a virtual terminal- allowing you to interact with the remote host. Telnet sends all messages in clear text and has no specific security mechanisms. Thus, in many applications and services, Telnet has been replaced by SSH in most implementations.


SHA-512: or Secure Hash Algorithm 512, is a hashing algorithm used to convert text of any length into a fixed-size string of 512 bits (64 bytes). Originally published in 2001, SHA-512 was developed by the US Government's National Security Agency (NSA).


SCP: A means of securely copying files. SCP allows you to copy files & directories from the current system to a remote system. Copy files & directories from a remote system to your current system. (Look up in Linuxpart3).


Python3 HTTPServer: Ubuntu machines come pre-packaged with python3. Python helpfully provides a lightweight and easy-to-use module called "HTTPServer". This module turns your computer into a quick and easy web server that you can use to serve your own files, where they can then be downloaded by another computing using commands such as curl and wget. 


