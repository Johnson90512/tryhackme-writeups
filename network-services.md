# Network Services

## Understanding SMB

    1. What does SMB stand for?    
        a. Server Message Block - A client-server communication protocol used for sharing access to files, printers, serial ports and other resources on a network.
    2. What type of protocol is SMB?
        a. response-request - It transmits multiple messages between the client and server to establish a connection.
    3. What do clients connect to servers using?    
        a. tcp/ip - Technically NetBIOS over TCP/IP
    4. What systems does Samba run on?
        a. Unix

## Enumerating SMB

    1. Conduct an nmap scan of your choosing, How many ports are open?
        a. 3 - The command that I used was 'sudo nmap -sS -vv -p- <ip address>' The output shows ports 22, 139, 445.
    2. What ports is SMB running on?
        a. 139/445
    3. Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name?
        a. WORKGROUP - The command I ran was 'enum4linux -A <ip address>' which does all the basic enumearation.
    4.What comes up as the name of the machine?        
        a. POLOSMB - - The same command from before was used for this one and the name of the machine was listed.
    5. What operating system version is running?    
        a. 6.1 - Listed in os version on the enum4linux output.
    6. What share sticks out as something we might want to investigate?    
        a. profiles - This was listed under Share Enumeration.

## Exploiting SMB

    1. What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?
        a. smbclient //10.10.10.2/secret -U suit -p 139
    2. Great! Now you've got a hang of the syntax, let's have a go at trying to exploit this vulnerability. You have a list of users, the name of the share (smb) and a suspected vulnerability.
        a. Y - The command used was 'smbclient //<ip address>/profiles -U Anonymous
    3. Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to?
        a. John Cactus - The information is in the "Working from home information.txt" file. I used the command 'get Working From Home Information.txt"' to get the file on my local machine to view.
    4. What service has been configured to allow him to work from home?
        a. ssh - the "Working From Home Information.txt" file explains that ssh is enabled
    5. Okay! Now we know this, what directory on the share should we look in?
        a. .ssh - the directory .ssh will contain information about connecting over ssh.
    6. This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us?
        a. id_rsa - This key is the private key that should not be shared. Access to this key is access to the server.
    7. Download this file to your local machine, and change the permissions to "600" using "chmod 600 [file]".

    Now, use the information you have already gathered to work out the username of the account. Then, use the service and key to log-in to the server.

    What is the smb.txt flag?
        a. THM{smb_is_fun_eh?} - To get this flag, you have to down loadthe file with the command 'get id_rsa', then once the file is on your local machine, you can run 'chmod 600 id_rsa' Once the permissions are set the final step is to connect over ssh with an identity file with the command 'ssh -i id_rsa cactus@<ip addr>' The username was found in the public key file as well.

## Understanding Telnet

    1. What is telnet?
        a. application protocol
    2. What has slowly replaced Telnet?
        a. ssh
    3. How would you connect to a Telnet server with the IP 10.10.10.3 on port 23?
        a. telnet 10.10.10.3 23
    4. The lack of what, means that all Telnet communication is in plaintext?
        a. encryption

## Enumerating Telnet

    1. How many ports are open on the target machine?    
        a. 1 - 'sudo nmap -sS -p- -vv -T5 <ip address>'
    2.  What port is this?
        a. 8012 - 'sudo nmap -sS -p- -vv -T5 <ip address>'
    3. This port is unassigned, but still lists the protocol it's using, what protocol is this?     
        a. tcp - 8012/tcp open  unknown syn-ack
    4. Now re-run the nmap scan, without the -p- tag, how many ports show up as open?
        a. 0 - The open port is above port 1000 so it wouldn't get checked.
    5, Based on the title returned to us, what do we think this port could be used for?
        a. a backdoor - The fingerprint shows the title Skidy's Backdoor
    6. Who could it belong to? Gathering possible usernames is an important step in enumeration.
        a. Skidy

## Exploiting Telnet

    1. Great! It's an open telnet connection! What welcome message do we receive?
        a. Skidy's Backdoor
    2. Let's try executing some commands, do we get a return on any input we enter into the telnet session? (Y/N)
        a. N
    3. Now, use the command "ping [local THM ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N)
        a. Y
    4. What word does the generated payload start with?
        a. mkfifo
    5. What would the command look like for the listening port we selected in our payload?
        a. nc -lvp 4444
    6. Success! What is the contents of flag.txt?
        a. THM{y0u_g0t_th3_t3ln3t_fl4g}

## Understanding FTP

    1. What communications model does FTP use?
        a. client-server
    2. What's the standard FTP port?
        a. 21
    3. How many modes of FTP connection are there?    
        a. 2 - Active and Passive
    
## Enumerating FTP

    1. Run an nmap scan of your choice.

    How many ports are open on the target machine?
        a. 2 - Ports 80 an 21.
    2. What port is ftp running on?
        a. 21 - This is the default port.
    3. What variant of FTP is running on it?
        a. vsftpd - 2.0.8 or later.
    4. What is the name of the file in the anonymous FTP directory?
        a. public_notice.txt
    5. What do we think a possible username could be?
        a. mike - This was in the notice.

## Exploiting FTP

    1. What is the password for the user "mike"?
        a. password - Using hydra we were able to crack the password. The command for this is 'hydra -t 4 -l mike -P /usr/share/wordlists/rockyou.txt -vV <ip address> ftp'
    2. What is ftp.txt?
        a. THM{y0u_g0t_th3_ftp_fl4g} - After connecting to the ftp server with the command above, the file was located in the root directory.

Further Reading:
- https://medium.com/@gregIT/exploiting-simple-network-services-in-ctfs-ec8735be5eef
- https://attack.mitre.org/techniques/T1210/
- https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/