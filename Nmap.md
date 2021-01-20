# Nmap

## Introduction

    1. What networking constructs are used to direct traffic to the right application on a server?
        a. ports
    2. How many of these are available on any network-enabled computer?
        a. 65535
    3. [Research] How many of these are considered "well-known"? (These are the "standard" numbers mentioned in the task)
        a. 1024

## Nmap Switches

    1. What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?
        a. -sS - sS is a TCP SYN scan, this is the default and most popular scan option.
    2. Which switch would you use for a "UDP scan"?
        a. -sU - This can be used to scan to find open UDP ports.
    3. If you wanted to detect which operating system the target is running on, which switch would you use?
        a. -O - Enable OS detection.
    4. Nmap provides a switch to detect the version of the services running on the target. What is this switch?
        a. -sV - Probe open ports to determine service/version info.
    5. The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?
        a. -v - Increase verbosity level.
    6. Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?
(Note: it's highly advisable to always use at least this option)
        a. -vv - Adding more V's increases the verbostiy even more.
We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients.

    7. What switch would you use to save the nmap results in three major formats?
        a. -oA - Output in the three major formats at once.
    8. What switch would you use to save the nmap results in a "normal" format?
        a. -oN - Output scan in Normal XML format.
    9. A very useful output format: how would you save results in a "grepable" format?
        a. -oG - Grepable format.
Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning.

    10. How would you activate this setting?
        a. -A - Aggressive mode.
Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!
    11. How would you set the timing template to level 5?
        a. -T5 - The 5 is the loudest timing, and 1 is the least aggressive.
We can also choose which port(s) to scan.
    12. How would you tell nmap to only scan port 80?
        a. -p 80
    13. How would you tell nmap to scan ports 1000-1500?
        a. -p 1000-1500 - This can be any range that you specify.
A very useful option that should not be ignored:
    14. How would you tell nmap to scan all ports?
        a. -p-
    15. How would you activate a script from the nmap scripting library (lots more on this later!)?
        a. --scripts
    16. How would you activate all of the scripts in the "vuln" category?
        a. --scripts=vuln - Instead of vuln, you can also specify other scripts.

## Scan Types - TCP Connect Scans

    1. Which RFC defines the appropriate behaviour for the TCP protocol?
        a. - RFC 793
    2. If a port is closed, which flag should the server send back to indicate this?
        a. rst - When a port is closed RFC 793 specifies that the port should reply with a TCP packet with the RST flag set.

## Scan Types - SYN Scans

    1.  There are two other names for a SYN scan, what are they?
        a. half-open, stealth - This is because they are often not detected.
    2. Can Nmap use a SYN scan without Sudo permissions (Y/N)?
        a. N - Nmap can only perform a SYN scan with root permissions.

## Scan Types - UDP Scans

    1.  If a UDP port doesn't respond to an Nmap scan, what will it be marked as?
        a. open|filtered - This is because it does not know that the port is for sure open, unless it gets a UDP response.
    2. When a UDP port is closed, by convention the target should send back a "port unreachable" message. Which protocol would it use to do so?
        a. icmp

## Scan Types - NULL, FIN, Xmas

    1.  Which of the three shown scan types uses the URG flag?
        a. xmas
    2. Why are NULL, FIN and Xmas scans generally used?
        a. Firewall evasion - because of how they react to closed ports and how a firewall reacts to this type of scan they are used to avoid them.
    3. Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?
        a. Microsoft Windows

## Scan Types - ICMP Network Scanning

    1.  How would you perform a ping sweep on the 172.16.x.x network (Netmask: 255.255.0.0) using Nmap? (CIDR notation)
        a. nmap -sn 172.16.0.0/16 - the command uses nmap with the -sn flag which tells nmap to not scan any ports and just icmp instead.

## NSE Scripts - Overview

    1.  What language are NSE scripts written in?
        a. Lua
    2. Which category of scripts would be a very bad idea to run in a production environment?
        a. intrusive - these are not safe and likely to affect the target.

## NSE Scripts - Working with the NSE

    1. What optional argument can the ftp-anon.nse script take?
        a. maxlist - This is seen from the script help menu.

## NSE Scripts - Searching for Scripts

    1. Search for "smb" scripts in the /usr/share/nmap/scripts/ directory using either of the demonstrated methods.
    What is the filename of the script which determines the underlying OS of the SMB server?
        a. smb-os-discovery.nse - I was able to find this with the command 'ls -al /usr/share/nmap/scripts/ | grep -i smb'
    2. Read through this script. What does it depend on?
        a. smb-brute - Running the command 'cat /usr/share/nmap/scripts/smb-os-discovery.nse | grep -i depend' shows that the scripts depends on the other script named above.

## Firewall Evasion

    1.  Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the -Pn switch?
        a. icmp
    2. [Research] Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?
        a. --data-length - Found on the nmap bypass firewalls and ids page. 

## Practical

    1. Does the target respond to ICMP (ping) requests (Y/N)?
        a. N - Running 'ping 10.10.129.251' did not get a reply.
    2.Perform an Xmas scan on the first 999 ports of the target -- how many ports are shown to be open or filtered?
        a. 999 - The command I ran was 'sudo nmap -Pn -sX -p 1-999 <ip address>'
    3. There is a reason given for this -- what is it?
    Note: The answer will be in your scan results. Think carefully about which switches to use -- and read the hint before asking for help!
        a. no responses
    4. Perform a TCP SYN scan on the first 5000 ports of the target -- how many ports are shown to be open?
        a. 5 - The scan I used was 'sudo nmap -vv -Pn -sT -p 1-5000 <ip address'
    5. Deploy the ftp-anon script against the box. Can Nmap login successfully to the FTP server on port 21? (Y/N)
        a. y - The script was able to login, but was unable to display the directory listing. The command that was used was 'sudo nmap -vv -Pn -sT -p 21 --script=ftp-anon <ip address'