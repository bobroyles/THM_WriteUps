# Find the flag.

## Map IP address and run nmap
    - sudo nano /etc/hosts 
    - nmap -T5 IP -sV -v
        - 80/tcp ; PHP cli server 5.5 or later (PHP 8.1.0-dev)
## gobuster to check for hidden directories 
    - Every request came back with code 200
## Looked up PHP version because it was outdated
    - Foundout this version was released with a backdoor for remote code execution
    - Exploit script found at: https://www.exploit-db.com/exploits/49933
    - Once I ran this short script and imported the target IP I had a reverse shell as root user
## Exploiting backdoor to find the flag
    - I was already root when entering the backdoor
    - ran a few commands (ls -la), tried to move around and couldn't
    - then just searched for a flag.txt (find / -name flag.txt 2>/dev/null)
    - found the flag
    - cat /flag.txt gave flag -> flag{4127d0530abf16d6d23973e3df8dbecb}