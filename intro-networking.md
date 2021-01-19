# Intro Networking

## Wireshark

    1. What is the protocol specified in the section of the request that's linked to the Application layer of the OSI and TCP/IP Models?
        a. Domain Name System - Wireshark works the OSI model from the bottom up, so the Physical layer is the first section of the wireshark detail section, and the Application is the last section.
    2. Which layer of the OSI model does the section that shows the IP address "172.16.16.77" link to (Name of the layer)?
        a. Netowrk - This layer is responsible for the logical addressing.
    3. In the section of the request that links to the Transport layer of the OSI and TCP/IP models, which protocol is specified?
        a. user datagram protocol - Located at the bottom of the network layer.
    4. Over what medium has this request been made (linked to the Data Link layer of the OSI model)?
        a . Ethernet II - This can be found in the second section of the wireshark details.
    5. Which layer of the OSI model does the section that shows the number of bytes transferred (81) link to?
        a. physical - This is the first section of wireshark.
    6. [Research] Can you figure out what kind of address is shown in the layer linked to the Data Link layer of the OSI model?
        a. mac - The data link layer deals with MAC addresses.

## Networking Tools - Ping

    1. What command would you use to ping the bbc.co.uk website?
        a. ping bbc.co.uk - The usage of this command is ping followed by the address you want to ping.
    2. What is the IPv4 address?
        a. 217.160.0.152 - This is the address that the DNS resolves to.
    3. What switch lets you change the interval of sent ping requests?
        a. -i - The description in the man pages says 'Wait interval in seconds between sending each packet.'
    4. What switch would allow you to restrict requests to IPv4?
        a. -4 - The man pages description says 'Use IPv4 only.'
    5. What switch would give you a more verbose output?
        a. -v - The man page description says 'Verbose output.'

## Networking Tools - Traceroute

    1. Can you see the path your request has taken?

    2. What switch would you use to specify an interface when using Traceroute?
        a. -i - The man pages description says 'Specifies  the interface through which traceroute should send packets.'
    3. What switch would you use if you wanted to use TCP SYN requests when tracing the route?
        a. -T - The man pages description says 'Use TCP SYN for probes'
    4. [Lateral Thinking] Which layer of the TCP/IP model will traceroute run on by default (Windows)?
        a. Internet - It runs on the osi networking layer, which is equal to the Internet layer on the TCP/IP model.

## Networking Tools - Whois

    1. Perform a whois search on facebook.com
        a.
    2. What is the registrant postal code for facebook.com?
        a. 94025 - The command 'whois facebook.com | grep -i postal' will display the postal codes in the whos command.
    3. When was the facebook.com domain first registered?
        a. 29/03/1997 - This can be found in the whos is with the command 'whois facebook.com | grep -i creation' and will be listed under Creation Date.
    4. Perform a whois search on microsoft.com
        a.
    5. Which city is the registrant based in?
        a. Redmond - To easily find this the command you can use is 'whois microsoft.com | grep -i city' which will display Registrant City.
    6. [OSINT] What is the name of the golf course that is near the registrant address for microsoft.com?
        a. Bellevue Golf Course - The command 'whois microsoft.com | grep -i street' will show the street address of the registrant, and looking on google maps we can see what the nearby golf course is.
    7. What is the registered Tech Email for microsoft.com?
        a. msnhst@microsoft.com - The command 'whois microsoft.com | grep -i email' will display a list of emails, and the Tech email is one of them.

## Networking Tools - Dig

    1. What is DNS short for?
        a. Domain Name System
    2. What is the first type of DNS server your computer would query when you search for a domain?
        a. recursive
    3. What type of DNS server contains records specific to domain extensions (i.e. .com, .co.uk*, etc)*? Use the long version of the name.
        a. Top-Level Domain
    4. Where is the very first place your computer would look to find the IP address of a domain?
        a. local cache
    5. [Research] Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one?
        a. 8.8.4.4
    6. If a DNS query has a TTL of 24 hours, what number would the dig query show?
        a. 86,400 - 24 hours * 60, to get the minutes, then 1440 * 60 to get the seconds.
    