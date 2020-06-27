# IP(Internet Protocol) Address

Every device connected to a network—computer, tablet, camera, whatever—needs a unique identifier so that other devices know how to reach it. In the world of TCP/IP networking, that identifier is the Internet Protocol (IP) address.

It looks something like `192.168.0.15`. An IP address is always a set of four numbers like that. Each number can range from 0 to 255. The combinations are 4.29 billion addresses. 

## TCP/IP

TCP/IP stands for Transmission Control Protocol/Internet Protocol. TCP/IP is a set of standardized rules that allow computers to communicate on a network such as the internet.

IP is the part that obtains the address to which data is sent. TCP is responsible for data delivery once that IP address has been found. TCP checks packets for errors and submits requests for re-transmissions if any are found.

Three of the most common TCP/IP protocols:
- HTTPS
- HTTP
- FTP 

[Example of a TCP/IP packet](https://www.computerhope.com/jargon/t/tcpip.htm).

Diff layers of TCP/IP:
- Network Access Layer : This layer is concerned with building packets. 
- Internet Layer : This layer uses IP (Internet Protocol) to describe how packets are to be delivered.
- Transport Layer : This layer utilizes UDP (User Datagram Protocol) and TCP (Transmission Control Protocol) to ensure the proper transmission of data.
- Application Layer : This layer deals with application network processes like HTTP.
### Subnetting 

Devices use another number called the subnet mask to distinguish the network and the host id. A common/common subnet mask is `255.255.255.0`. The position of the changes from 255 to 0 indicate the division between the network and host ID. The 255s “mask out” the network ID from the equation. People often use custom subnet masks to create multiple subnets on the same network.

Subnetting is a network design strategy that segregates a larger network into smaller components. While connected through the larger network, each subnetwork — or subnet — functions with a unique IP address. 

Splitting network sectors into a series of subnet components has a couple of practical advantages. First, by segregating the larger network into distinct but interconnected subsections, it is often easier to isolate performance issues and repair one of these subsections without having to shut down the functions taking place in the others. The process of subnetting can also enhance the process of maintaining the overall network, making it possible to perform diagnostics or other testing without slowing down or impacting the functionality of other components that make up the larger network. [here](https://www.wisegeek.com/what-is-subnetting.htm).

[This has a good explanation](https://www.webopedia.com/TERM/S/subnet_mask.html).

### The Default Gateway Address

Depending on the platform you’re using, this address might be called something different. It’s sometimes called the “router,” “router address,” default route,” or just “gateway.” These are all the same thing. It’s the default IP address to which a device sends network data when that data is intended to go to a different network (one with a different network ID) than the one the device is on.

## Difference Between IPv4 and IPv6

In the mid-90s, worried about the potential shortage of IP addresses, the internet Engineering Task Force (IETF) designed IPv6. IPv6 uses a 128-bit address instead of the 32-bit address of IPv4.

IPv6 addresses are expressed as eight number groups, divided by colons. Each group has four hexadecimal digits.

The thing is, the shortage of IPv4 addresses that caused all the concern ended up being mitigated to a large extent by the increased use of private IP addresses behind routers. These priavte IP's arent exposed publicly. So, even though IPv6 is still a major player and that transition will still happen, it never happened as fully as predicted—at least not yet.  

## How does a device get an IP Address ?

There are really two types of IP assignments: dynamic and static.

A dynamic IP address is assigned automatically when a device connects to a network using DHCP(Dynamic Host Configuration Protocol).

When a device connects to the network, it sends out a broadcast message requesting an IP address. DHCP intercepts this message, and then assigns an IP address to that device from a pool of available IP addresses.

The thing about dynamic addresses is that they can sometimes change. DHCP servers lease IP addresses to devices, and when those leases are up, the devices must renew the lease.

One can also manually set an IP Address ?

## Who owns IP Addresses ?

ICANN (Internet Corporation for Assigned Names and Numbers) is the one responsible for creating and distributing IP addresses. So, ICANN is the initial owner of every IP address. From there, the IP addresses reach IANA (Internet Assigned Numbers Authority), which is a function of ICANN and which is responsible for the global coordination of the DNS Root, IP addressing, and other internet protocol resources.


## Public vs Private Addresses:

A public IP address is assigned to a device so it can directly connect to the internet. Any device that can be accessed directly on the internet, being it a smartphone, web server, or email server, has a unique public IP address.

Private IP addresses are used in homes or organizations. Your internet router has a public IP address which makes it possible to connect to the internet, but the devices you have around the house like your smartphone or printer can have private IP addresses. Meaning they can only communicate with each other over the same network but someone from the outside is not able to reach them. For example, your printer has a private IP address so only the people in the house can use it for printing.

## What does your IP address reveal about you?

An IP address reveals an approximate physical location of your device (if you’re not using a VPN or proxy). If you go to an IP checker tool, you’ll see that it shows the region you’re in, and often the city and zip code. These details are not always accurate as it may show you being km away from your actual location. 

Your device can be hacked with the IP address only if there are also other vulnerabilities like an unsecured router, open ports, no firewall, or you’re accessing a website or program that has vulnerabilities. The most common attack using IP addresses is the DDOS attack.

But even though someone might not hack your device using the IP address, he can still find out your location.

The most efficient way to keep yourself safe online is to hide your real IP address. You can easily do this by using a proxy or a VPN service.

## VPNs and Proxies 

- [Comparing VPNs and Proxies](https://drsoft.com/2018/09/26/vpn-vs-proxy/) - one should defintely use a VPN for more security. 

## What is a MAC Address ?

More and more people created their own private networks, using those pece of hardware on your local network has a MAC address in addition to the IP address assigned to it by the local router or server. 

A MAC(Media Access Control Address) address is a number assigned to the NIC(Netowrk Interface Card) card by the manufacturer. A MAC address uniquely identifies a device that wants to take part in a network. The IP address identifies a connection to a device in a network.

MAC address is a 48-bit hexadecimal address. MAC address is used at the data link layer of OSI/TCP/IP model.  

[Diff. between mac address and IP address](https://techdifferences.com/difference-between-mac-and-ip-address.html). 

 
