# Linux Fundamentals Part 3

## Section 5: Advanced File Operations - cd && mkdir

    1. Using relative paths, how would you cd to your home directory?
        a. cd ~ - cd will change the directory to the location following, and ~ is the home directory.
    2. Using absolute paths how would you make a directory called test in /tmp?
        a. mkdir /tmp/test - Using mkdir to make a directory to a supplied directory path.

## Section 5: Advanced File Operations - ln

    1. How would I link /home/test/testfile to /tmp/test?
        a. ln /home/test/testfile /tmp/test - ln is the program followed by the source and destination paths to link together.

## Section 5: Advanced File Operations - find

    1. How do you find files that have specific permissions?
        a. -perm - This flag allows you search files and specify the permissions you are looking for. There are 4 different perm modes.
    2.How would you find all the files in /home?
        a. find /home - This is simple by funning the command find followed by the directory.
    3. How would you find all the files owned by paradox on the whole system?
        a. find / -user paradox - Using the man pages, there is a -user flag that allows us to search all files based on the user.

## Section 5: Advanced File Operations - grep

    1. What flag lists line numbers for every string found?
        a. -n - Reading the man pages for grep, the description for this is 'Prefix each line of output with the 1-based line number within its input file.
    2. How would I search for the string boop in the file aaaa in the directory /tmp?
        a. grep boop /tmp/aaaa - This command is broken down into 3 groups the program name, the search pattern, and the search location.

## Binary - Shiba3

    1. What is shiba4's password?
        a. test1234 - Using mkdir ~/test will make a test directory in your home directory. Then using touch ~/test/test1234 will make the test1234 file in that directory. Finally you have to find the shiba4 binary, to do this use the command find / * | grep shiba4 | grep -v "Permission denied".

## Section 6: Miscellaneous - sudo

    1. How do you specify which user you want to run a command as?
        a. -U - Using the man pages for sudo will show the description for -U to be 'Used in conjunction with the -l option to list the privileges for user instead of for the invoking user.
    2. How would I run whoami as user jen?
        a. sudo -U jen whoami - The command breaks down to the program 'sudo', followed by the user flag, then the specified user, and finally the command that is to be run as that user.
    3. How do you list your current sudo privileges(what commands you can run, who you can run them as etc.)
        a. -l - Reading  the man pages for sudo, the description says 'list the allowed (and forbidden) commands for the invoking user'

## Section 6: Miscellaneous - Adding users and groups

    1. How would I add the user test to the group test?
        a. sudo usermod -a -G test test - The breakdown of this command is sudo to make sure you have the correct permissions, usermod to run the program, -a means to add, -G is adding a group, test is the group name, and test is the username to add to the group.
