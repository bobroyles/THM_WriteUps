# Find the first secret ingredient 
## Starting 
  - add thm to list of known hosts, sudo nano /etc/hosts
  - run nmap scan for open ports
  - inspect page source while nmap is running
    - HTML comment saying not to forget username: R1ckRul3s
  - nmap returned two open ports, 22/tcp ssh and 80/txp http
## Further enumeration 
  - next I ran gobuster on the IP to search for any hidden directories
  - there was a text file, robots.txt
    - robots.txt just said 'Wubbalubbadubdub'
  - I then ran gobuster again because I realized I forgot to search for the .php extension
  - found a login.php and portal.php
  - On the login.php page I was able to login using the username from the HTML comment and the string from robots.txt
### After Logging in 
  - There was a command panel that I found allowed command execution after running 'ls -la'
  - this gave way to a "supersecretpickleingredient.txt" file with the first ingredient
  - first ingredient: mr. meeseek hair
# Second Ingredient and Third Ingredient
## Escalating privileges for final two flags
  - Once I had command input availability I began to try and execute any commands I could
  - Several commands were blocked so I attempted to create a reverse shell and escalated privileges from there
  - First tried using a bash script with a listener but this didn't work
  - Next I tried python and found I could run python3 code
  - I think used a pentest monkey reverse shell code found here: https://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
  - using the nc listener and python script I had gotten my reverse shell
  - once in the shell i used 'sude bash' and was able to escalate to root without trouble
  - Searched system to find the last two ingredients
  - Second flag was in 'rick' dir under 'second ingredients': 1 juicy tear
  - Third flag in '3rd.txt': fleeb juice
