# Linux Fundamentals Part 2

## Section 4: Linux Operators - $

    1. How would you set nootnoot equal to 1111?
        a. export nootnoot=1111 - This is setting the environment variable nootnoot to 1111 the challenge reading shows us how to do this.
    2. What is the value of the home environment variable?
        a. /home/shiba2 - The home environment can be displayed by typing 'echo $HOME' into the command line, which is the command to display environment variables.

## Section 4: Linux Operators - >

    1. How would you output twenty to a file called test?
        a. echo twenty > test - Echo just repeats the text of twenty to the commandline and the > character redirects it to the file specified.

## Binary - shiba2

    1. What is shiba3's password?
        a. happynootnoises - To get the password from the binary you have to set an environment variable of test1234 equal to $USER environment variable, the command to do that is export test1234=$USER

## Section 5: Advanced File Operation - chown

    1. How would you change the owner of file to paradox?
        a. chown file paradox - The command is chown followed by the name of the file then the user you would like to make the owner.
    2. What about the owner and the group of file to paradox?
        a. chown paradox:paradox file - The command for this is chown followed by the owner:group and then the file name.
    3. What flag allows you to operate on every file in the directory at once?
        a. -R - Looking at the man pages for chown the description for -R is 'operate on files and firectories recursively'

## Section 5: Advanced File Operations - chmod

    1. What permissions mean the user can read the file, the group can read and write to the file, and no one else can read, write or execute the file?
        a. 460 - Using the permissions chart in the challenge notes 4 is user can read, 6 is group can read and write, 0 is everyone else can do nothing.
    2. What permissions mean the user can read, write, and execute the file, the group can read, write, and execute the file, and everyone else can read, write, and execute the file?
        a. 777 - Using the permissions chart in the challenge notes, 7 is user can read write and execute, second 7 is group can read wrtie and execute, and third 7 means everyone can read write and execute.

## Section 5: Advanced File Operations - rm

    1. What flag deletes every file in a directory?
        a. -r - In the man pages the description for -r is 'remove directories and their contents recursively'.
    2. How do you suppress all warning prompts?
        a. -f - In the man pages the description for -f is 'ignore nonexistent files and arguments, never prompt'.

## Section 5: Advanced File Operations - mv

    1. How would you move file to /tmp?
        a. mv file /tmp - The command is structured that mv to call the move program, followed by the name of the file, and followed by the new location for that file.
