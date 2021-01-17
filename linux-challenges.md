# Linux Challenges

Test your Linux skills by finding flags using various Linux commands and concepts. Do you have what it takes to solve these challenges?

## Linux Challenges Introduction
    
    Username: garry
    Password: letmein
    1. How many visible files can you see in garrys home directory?
        a. 3 - Running ls shows only 3 files in this directory.

## The Basics

    1. What is flag 1?
        a. f40dc0cff080ad38a6ba9a1c2c038b2c - Running cat flag1.txt will display the output of the file.
    
    Username:bob
    Password:linuxrules
    
    2. What is flag 2?
        a. 8e255dfa51c9cce67420d2386cede596 - Log into the user account for bob using 'su bob', then change directories to the new users home directory. Run cat on the file flag2.txt that is located in this directory.
    3. Flag 3 is located where bob's bash history gets stored?
        a. 9daf3281745c2d75fc6e992ccfdedfcd - Run 'ls -al' and it will show a file called .bash_history, run cat on this file and you will see the flag at the top of the file.
    4. Flag 4 is located where cron jobs are created?
        a. dcd5d1dcfac0578c99b7e7a6437827f3 - Cronjobs are created with crontab, running crontab -e will show the contens of the crontab file. Crontab is located at /usr/local/bin/crontab.
    5. Find and retrieve flag 5?
        a. bd8f33216075e5ba07c9ed41261d1703 - To find flag 5 we will use the find command. The command is 'find / * | grep flag5 | grep -v "Permission denied".
    6. "Grep" through flag 6 and find the flag. The first 2 characters of the flag is c9?
        a. c9e142a1e25b24a837b98db589b08be5 - First we need to locate the file flag.txt, to find it we use the same command as last time 'find / * | grep flag5 | grep -v "Permission denied". The next step is to use grep to search within this file. The command for this is 'cat /home/flag6.txt | grep c9'. 
    7. Look at the systems processes. What is flag 7?
        a. 274adb75b337307bd57807c005ee6358 - To find this flag you need to be able to look at the system processes with the 'ps aux | grep flag7' command.
    8. De-compress and get flag 8?
        a. 75f5edb76fe98dd5fc9f577a3f5de9bc - To find this flag we have to locate it with 'find / * | grep flag8 | grep -v "Permission denied"'. Then once you have the flag you have to extract it with the command 'tar -xvf /home/bob/flag8.txt'
    9. By look in your hosts file, locate and retrieve flag 9?
        a. dcf50ad844f9fe06339041ccc0d6e280 - Hosts files are located at /etc/hosts in linux. Cat this file and locate the flag.
    10. Find all other users on the system. What is flag 10?
        a. 5e23deecfe3a7292970ee48ff1b6d00c - Users are in /etc/passwd file. Cat this file and locate the user that is a 32bit flag.
## Linux Functionality
    1. Run the command flag11. Locate where your command alias are stored and get flag 11?
        a. b4ba05d85801f62c4c0d05d3a76432e0 - Alias are stored in the ~/.bashrc file. Using the command 'cat ~/.bashrc | grep flag11' the flag gets displated in the commands for the alias flag11.
    2. Flag12 is located were MOTD's are usually found on an Ubuntu OS. What is flag12?
        a. 01687f0c5e63382f1c9cc783ad44ff7f - The flag is located in the motd folder which in Ubuntu can be seen with 'cat /etc/update-motd.d/00-header'.
    3.Find the difference between two script files to find flag 13?
        a. 3383f3771ba86b1ed9ab7fbf8abab531 - The flag13 folder is located in ~/flag13, move into this folder and run the command 'diff script1 script2' to output the flag.
    4. Where on the file system are logs typically stored? Find flag 14?
        a. 71c3a8ad9752666275dadf62a93ef393 - Flags in linux are normally stored in /var/log. On this server there is a file called /var/log/flagtourteen.txt, which is an executeable and needs to be run to get the flag.
    5.Can you find information about the system, such as the kernel version etc? Find flag 15.
        a. a914945a4b2b5e934ae06ad6f9c6be45 - To find this use the command 'cat /etc/*release*'. The info is in the file lsb-release but using the command above shows all release information.
    6. Flag 16 lies within another system mount.
        a. cab4b7cae33c87794d82efa1e7f834e6 - This flag was tricky if you don't know where to look. System mounts are often located in /media folder, once navigating to this folder you will realize that there are sub folders spelling out the word flag, then a folder with the flag name.
    7. Login to alice's account and get flag 17. Her password is TryHackMe123
        a. 89d7bce9d0bab49e11e194b54a601362 - Login to alice's account using 'su alice' and then change to alice's home directory. The flag is in the home directory and can be read from there.
    8. Find the hidden flag 18.
        a. c6522bb26600d30254549b6574d2cef2 - Hidden files can be found using the command 'ls -al'. Run this command in alices home directory and you will find the hidden flag represented by a . before the filename. 
    9. Read the 2345th line of the file that contains flag 19.
        a. 490e69bd1bf3fc736cce9ff300653a3b - This flag can be found using the command 'cat -n flag19 | grep 2345'. By using the -n flag for cat it will number all of the output lines of the file. Then using grep we search for the specific line number.

## Data Representation, Strings and Permissions

    1. Find and retrieve flag 20.
        a. 02b9aab8a29970db08ec77ae425f6e68 - The flag file is located in the home directory for alice, but when the file is read it doesn't look like all the other flags do. By looking at the last character we can be pretty sure that the text is encoded in base64. The command to get the flag is 'cat flag20 | base64 --decode'
    2. Inspect the flag21.php file. Find the flag.
        a. g00djob - Running the program strings on this file will display the flag. The command for this is 'strings flag21.php'
    3. Locate and read flag 22. Its represented as hex.
        a. 9d1ae8d569c83e03d8a8f61568a0fa7d - This flag needs to be converted from hex to ascii. This can be done with a program called cyberchef, or it can be done with xxd. The command 'cat flag22 | xxr -r' only displays part of the correct output because it is in continuous hexdump style. So the correct command is 'cat flag22 | xxd -r -p'.
    4. Locate, read and reverse flag 23.
        a. ea52970566f4c090a7348b033852bff5 - The flag can be read, and reversed by hand but lets use a command line program. 'cat flag23 | rev' 
    5. Analyse the flag 24 compiled C program. Find a command that might reveal human readable strings when looking in the machine code code.
        a. hidd3nStr1ng - This flag is found using the program strings, it can be found using  the command 'strings flag24'
    6. Flag 25 does not exist.
        a. No flag just complete
    7. Find flag 26 by searching the all files for a string that begins with 4bceb and is 32 characters long. 
        a. 4bceb76f490b24ed577d704c24d6955d - As with most linux tools, there is more than one way to solve this challenge. The way I used was with the command grep / -rne "4bceb" 2>&-, but after looking on line to see if there are better ways for this to be done (my way took a long time), find / -xdev -type f -print0 2>/dev/null | xargs -0 grep -E '^[a-z0-9]{32}$' 2>/dev/null
    8. Locate and retrieve flag 27, which is owned by the root user.
        a. 6fc0c805702baebb0ecc01ae9e5a0db5 - you can see which commands a user can run as sudo with sudo -l. This will show the exact commands the user alice can run.
    9. Whats the linux kernel version?
        a. 4.4.0-1075-aws
    10. Find the file called flag 29 and do the following operations on it:
    Remove all spaces in file.
    Remove all new line spaces.
    Split by comma and get the last element in the split.
        a. fastidiisuscipitmeaei - First you have to locate the file, it is in /home/garry/ . To get the flag the following command needs to be run "cat /home/garry/flag29 | tr -d ' \t\n\r' | tr ',' '\n'" . What this command will do is output the contents of the file, delete the tab newline and return character, then tr replaces all the commas with a newline character. The last element is the flag.

## SQL, FTP, Groups and RDP
    1. Use curl to find flag 30.
        a. fe74bb12fe03c5d8dfc245bdd1eae13f - The command to solve this flag is 'curl localhost'. Curl allows you to be able to interact with a URL.
    2. Flag 31 is a MySQL database name.
    MySQL username: root
    MySQL password: hello
        a. 2fb1cab13bf5f4d61de3555430c917f4 - To find this flag, you need to log into mysql as root. The command to do this is 'mysql -uroot -phello' you'll notice there are no spaces between the -u and the username and -p and password. To look at the database names, use the command 'show databases;' The database name is database_2fb1cab13bf5f4d61de3555430c917f4.
    3. Bonus flag question, get data out of the table from the database you found above!
        a. ee5954ee1d4d94d61c2f823d7b9d733c - To find the bonus flag, use the command 'use database_2fb1cab13bf5f4d61de3555430c917f4;' then look at the tables that are in this database with 'show tables;'. The next thing is to show the information in the table flags with the command 'select * from flags;' which will output the flag.
    4. Using SCP, FileZilla or another FTP client download flag32.mp3 to reveal flag 32.
        a. tryhackme1337 - Open a new terminal window on your local machine. To download the file use the command 'scp alice@<remoteIP>:/home/alice/flag32.mp3 .' this will place it in your current directory.
    5. Flag 33 is located where your personal $PATH's are stored.
        a. 547b6ceee3c5b997b625de99b044f5cf - This is a little confusing as it doesn't tell you the current user isn't correct. Change users to bob and look in the .profile file in the home directory to get the flag.
    6. Switch your account back to bob. Using system variables, what is flag34?
        a. 7a88306309fe05070a7c5bb26a6b2def
    7. Look at all groups created on the system. What is flag 35?
        a. 769afb6 - Groups are stored in /etc/group, looking in this folder will give you the flag.
    8. Find the user which is apart of the "hacker" group and read flag 36.
        a. 83d233f2ffa388e5f0b053848caed1eb - In the group folder from the last question, using grep to isolate the group hacker it shows that bob is the user in this group. Using find the flag is located in /etc/flag36.