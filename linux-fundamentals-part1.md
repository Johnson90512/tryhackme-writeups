# Linux Fundamentatls Part 1

## Section 2: Running Commands - Manual Pages and Flags

    1. How would you output hello without a newline?
        a. echo -n hello - If we read the man pages the -n flag is described to no output the trailing newline.

## Section 3: Basic File Operations - ls

    1. What flag outputs all entries?
        a. -a - The answer to this can be seen in the cahllanege description, it tells us that the -a flag shows all files/directories.
    2. What flag outputs things in a "long list" format?
        a. -l - If we read the man pages for ls, we see that the description for -l is 'use a long listing format'.

## Section 3: Basic File Operation - cat

    1. What flag numbers all output lines?
        a. -n - If we read the man ages for ls, we see that the description for -n is 'number all output lines'.

## Section 3: Basic File Operations - Running a Binary

    1. How would you run a binary called hello using the directory shortcut . ?
        a. ./hello - The answer to this is actually given to us in the challnege reading telling us that using the. is referrrng to the current directory.
    2. How would you run a binary called hello in your home directory using the shortcut ~ ?
        a. ~/hello - Using the ~/ shortcut takes us to the home directory and then it will look for whatever is after the /, this can also be found in the challenge reading.
    3. How would you run a binary called hello in the previous directory using the shortcut .. ?
        a. ../hello - The two . in a row is a shortcut to reference the previous directory, and can be seen in the challenge reading.

## Binary - Shiba1

    1. What's the password for shiba2?
        a. pinguftw - The password can be found by running the binary shiba1. The binary won't do anything though until you create a file in the same directory called noot.txt.
## su

    1. How do you specify which shell is used when you login?
        a. -s - The description in the man pages for su state that -s is 'The shell that will be invoked.