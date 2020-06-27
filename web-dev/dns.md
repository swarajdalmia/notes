# Domain Name and DNS Servers

Alongside a device’s IP address, subnet mask, and default gateway address: the addresses of one or two default Domain Name System (DNS) servers. 

DNS works kind of like a phone book, looking up human-readable things like website names, and converting those to IP addresses. DNS does this by storing all that information on a system of linked DNS servers across the internet. 

On a typical small or home network, the DNS server IP addresses are often the same as the default gateway address. 

Devices send their DNS queries to your router, which then forwards the requests on to whatever DNS servers the router is configured to use. By default, these are usually whatever DNS servers your ISP provides, but you can change those to use different DNS servers if you want. Sometimes, you might have better success using DNS servers provided by third parties, like Google or OpenDNS.
