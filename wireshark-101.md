# Wireshark 101

Learn the basics of Wireshark and how to analyze various protocols and PCAPs

## ARP Traffic

    1. What is the Opcode for Packet 6?
        a. request (1)
    2. What is the source MAC Address of Packet 19?
        a. 80:fb:06:f0:45:d7
    3. What 4 packets are Reply packets?
        a. 76,400,459,520
    4. What IP Address is at 80:fb:06:f0:45:d7?
        a. 10.251.23.1

## ICMP Traffic

    1. What is the type for packet 4?
        a. 8
    2. What is the type for packet 5?
        a. 0
    3. What is the timestamp for packet 12, only including month day and year?
        a. May 30, 2013
    4. What is the full data string for packet 18?
        a. 08090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f202122232425262728292a2b2c2d2e2f3031323334353637
    
## DNS Traffic

    1. What is being queried in packet 1?
        a. 8.8.8.8.in-addr.arpa
    2.  What site is being queried in packet 26? 
        a. www.wireshark.org
    3. What is the Transaction ID for packet 26?
        a. 0x2c58

## HTTP Traffic

    1. What percent of packets originate from Domain Name System?
        a. 4.7
    2. What endpoint ends in .237?
        a. 145.254.160.237
    3. What is the user-agent listed in packet 4?
        a. Mozilla/5.0 (Windows; U; Windows NT 5.1; en-US; rv:1.6) Gecko/20040113
    4. Looking at the data stream what is the full request URI from packet 18?
        a. http://pagead2.googlesyndication.com/pagead/ads?client=ca-pub-2309191948673629&random=1084443430285&lmt=1082467020&format=468x60_as&output=html&url=http%3A%2F%2Fwww.ethereal.com%2Fdownload.html&color_bg=FFFFFF&color_text=333333&color_link=000000&color_url=666633&color_border=666633
    5. What domain name was requested from packet 38?
        a. www.ethereal.com
    6. Looking at the data stream what is the full request URI from packet 38?
        a. http://www.ethereal.com/download.html

## HTTPS Traffic

    1. Looking at the data stream what is the full request URI for packet 31?
        a. https://localhost/icons/apache_pb.png
    2. Looking at the data stream what is the full request URI for packet 50?
        a. https://localhost/icons/back.gif
    3. What is the User-Agent listed in packet 50?
        a. Mozilla/5.0 (X11; U; Linux i686; fr; rv:1.8.0.2) Gecko/20060308 Firefox/1.5.0.2
