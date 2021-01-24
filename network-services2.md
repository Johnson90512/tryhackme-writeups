# Network Services 2

## Understanding NFS
    NFS Resources - https://docs.oracle.com/cd/E19683-01/816-4882/6mb2ipq7l/index.html

    1. What does NFS stand for?
        a. Network File System.
    2. What process allows an NFS client to interact with a remote directory as though it was a physical device?
        a. mounting - It mounts all or part of a file system on a server.
    3. What does NFS use to represent files and directories on the server?
        a. file handles - This uniquely identifies each file and directory that is on the server.
    4. What protocol does NFS use to communicate between the server and client?
        a. rpc - It takes the parameters the file handle, the name of the file to be accessed, the user's user ID, the user's group ID
    5. What two pieces of user data does the NFS server take as parameters for controlling user permissions? Format: parameter 1 / parameter 2
        a. user id / group id - More parameters listed in question 4.
    6. Can a Windows NFS server share files with a Linux client? (Y/N)
        a. Y 
    7. Can a Linux NFS server share files with a MacOS client? (Y/N)
        a. Y
    8. What is the latest version of NFS? [released in 2016, but is still up to date as of 2020] This will require external research.
        a. 4.2 - Information was found here: https://en.wikipedia.org/wiki/Network_File_System#NFSv4

## Enumerating NFS

    1. Conduct a thorough port scan scan of your choosing, how many ports are open?
        a. 7 - Using the command 'sudo nmap -sSV -vv -p- -T5 <ip address>' to scan all ports to get their version.
    2.Which port contains the service we're looking to enumerate?
        a. 2049 - The service that is running is nfs_acl.
    3. Now, use /usr/sbin/showmount -e [IP] to list the NFS shares, what is the name of the visible share?
        a. /home - Running the command '/usr/sbin/showmount -e <ip address>' this will list the nfs shares on the server. 
    4. What is the name of the folder inside?
        a. cappucino - Using the command 'sudo mount -t nfs 10.10.147.144:/home -nolock /tmp/mount/' to mount the share.
    5. Interesting! Let's do a bit of research now, have a look through the folders. Which of these folders could contain keys that would give us remote access to the server?
        a. .ssh
    6. Which of these keys is most useful to us?
        a. id_rsa
    7. Can we log into the machine using ssh -i <key-file> <username>@<ip> ? (Y/N)
        a. Y

## Exploiting NFS

    1. Now, we're going to add the SUID bit permission to the bash executable we just copied to the share using "sudo chmod +[permission] bash". What letter do we use to set the SUID bit set using chmod?
        a. s - This is told by the s bit at the beginning of permissions using ls -al. 
    2.  Let's do a sanity check, let's check the permissions of the "bash" executable using "ls -la bash". What does the permission set look like? Make sure that it ends with -sr-x.
        a. rwsr-sr-x
    3. Great! If all's gone well you should have a shell as root! What's the root flag?
        a. THM{nfs_got_pwned} - root.txt is located at /root/root.txt

## Understanding SMTP

    1. What does SMTP stand for?
        a. Simple Mail Transfer Protocol.
    2. What does SMTP handle the sending of?
        a. emails.
    3. What is the first step in the SMTP process?
        a. SMTP handshake
    4.  What is the default SMTP port?
        a. 25
    5. Where does the SMTP server send the email if the recipient's server is not available?
        a. smtp queue
    6.  On what server does the Email ultimately end up on?
        a. POP/IMAP
    7. Can a Linux machine run an SMTP server? (Y/N)
        a. Y
    8. Can a Windows machine run an SMTP server? (Y/N)
        a. Y

## Enumerating SMTP

    1.First, lets run a port scan against the target machine, same as last time. What port is SMTP running on?
        a. 25
    2. Okay, now we know what port we should be targeting, let's start up Metasploit. What command do we use to do this? 
        a. msfconsole
    3.  Let's search for the module "smtp_version", what's it's full module name?
        a. auxiliary/scanner/smtp/smtp_version
    4. Great, now- select the module and list the options. How do we do this?
        a. options- You can also use the command 'show options'
    5. Have a look through the options, does everything seem correct? What is the option we need to set?
        a. RHOSTS - This is the only option that doesn't have something set on it.
    6. What Mail Transfer Agent (MTA) is running the SMTP server? This will require some external research.
        a. postfix - This can also be seen from the output of metasploit
    7.  Good! We've now got a good amount of information on the target system to move onto the next stage. Let's search for the module "smtp_enum", what's it's full module name? 
        a. auxiliary/scanner/smtp/smtp_enum - Found using the command search smtp_enum
    8.What option do we need to set to the wordlist's path?
        a. user_file
    9.Once we've set this option, what is the other essential paramater we need to set?
        a. RHOSTS
    10. Okay! Now that's finished, what username is returned?
        a. administrator

## Exploiting SMTP

    1. What is the password of the user we found during our enumeration stage?
        a. alejandro
    2. Great! Now, let's SSH into the server as the user, what is contents of smtp.txt
        a. THM{who_knew_email_servers_were_c00l?}

## Understanding MySQL

    1. What type of software is MySQL?
        a. relational database management system
    2. What language is MySQL based on?
        a. SQL - Structured Query Language
    3. What communication model does MySQL use?
        a. client-server
    4. What is a common application of MySQL?
        a. back end database
    5. What major social network uses MySQL as their back-end database? This will require further research.
        a. facebook

## Enumerating MySQL

    1.  As always, let's start out with a port scan, so we know what port the service we're trying to attack is running on. What port is MySQL using?
        a. 3306 - This is the default port for mysql
    2.  Search for, select and list the options it needs. What three options do we need to set? (in descending order).
        a. password/ rhosts/username
    3.  Run the exploit. By default it will test with the "select module()" command, what result does this give you?
        a. 5.7.29-0ubuntu0.18.04.1
    4. Great! We know that our exploit is landing as planned. Let's try to gain some more ambitious information. Change the "sql" option to "show databases". how many databases are returned?
        a. 4

## Exploiting MySQL
    users - root:password
            carl

    1. First, let's search for and select the "mysql_schemadump" module. What's the module's full name?
        a. auxiliary/scanner/mysql/mysql_schemadump
    2.  Great! Now, you've done this a few times by now so I'll let you take it from here. Set the relevant options, run the exploit. What's the name of the last table that gets dumped?
        a. waits_global_by_latency
    3.  Awesome, you have now dumped the tables, and column names of the whole database. But we can do one better... search for and select the "mysql_hashdump" module. What's the module's full name? 
        a. auxiliary/scanner/mysql/mysql_hashdump
    4. Again, I'll let you take it from here. Set the relevant options, run the exploit. What non-default user stands out to you?
        a. carl
    5. Now, we need to crack the password! Let's try John the Ripper against it using: "john hash.txt" what is the password of the user we found? 
        a. doggie
    6. Awesome. Password reuse is not only extremely dangerous, but extremely common. What are the chances that this user has reused their password for a different service?
    What's the contents of MySQL.txt
        a. THM{congratulations_you_got_the_mySQL_flag}

## Further Reading

    https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-sg-en-4/ch-exploits.html
    https://www.nextgov.com/cybersecurity/2019/10/nsa-warns-vulnerabilities-multiple-vpn-services/160456/
