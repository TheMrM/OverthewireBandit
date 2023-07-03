This is the Walktrough of Bandit

For first challange bandit0 -> bandit1 :

We log on using command ssh -p 2220 bandit0@bandit.labs.overthewire.org
The user and pw was provided on website.
We found a file 'readme' that we opend with 'cat readme'. Inside it contained
the PW for the next level.

We log on using command ssh -p 2220 bandit1@bandit.labs.overthewire.org
There is a '-' file. It can be read by using 'head ./-', found the pw for next level

#We are not going to show the command to login anymore, should be self explanitory from now on how to login. I am going to write only about the method used to solve the challange

 bandit2 we have "space in the filename" file that we open with 'cat'
and we find the password

 bandit3 we have a ".hidden" file. We used 'cat ./.hidden' to find the
password

 bandit4 we used "find -type f | xargs file | grep text" that will display the file that contains ASCII text. Then we open the file using "cat ./-file" and it shows us the pwd

 bandit5 we used "find -type f -size 1033c -non -executable -exec ls -lh {} +" in order to find a human-readable, 1033 bytes in size, not executable file. Then we open it with "cat"

 bandit6 we used "find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null" that fits the fallowing criteria : owned by user bandit7, owned by group bandit6, 33 bytes in size. It shows the full path to the file that we are looking for and then we open the file with "cat file_path" and we get the pwd for next level

 bandit7 we used "grep "millionth" data.txt" to find pwd next to the word in the file

 bandit8 we first used 'grep -o '.*' data.txt' to extract each line. Then we added ' | sort' . Finally we used the 'uniq -u' option to display the unique lines that occur only once. Final command was "grep -o '.*' data.txt | sort | uniq -u" and we found the password

 bandit9 we combined 'strings' and 'grep' in "strings data.txt | grep "^==.*$" " and it showed the password. The "^==.*$" pattern matches the lines that started with == followed by any number of chars. This pattern is used to find lines preceded by several '=' chars

 bandit10 we simpy used "base64 -d" that decodes the file and shows the password for next level 

 bandit11 we rotated by 13 positions, with the 'tr' command.
We used to decode "tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt" and it prints out the password


 bandit12 we firs went to the file "/home/bandit13" where we found a ssh private key file call "sshkey.private". Then we keep using "file" to inspect the type of data, then we keep extracting it based on what type of 'data' is. Also we need to "mv" file as ".g". Ex: mv data8.bin data8.bin.gz . We keep doing it so until we have a ASCII text file.

 bandit13 we manage to login to bandit14 by simply using "ssh -i file_found bandit14@localhost" and it connected us to the next level. It was possible since the "file_found" contained the SSH key of bandit14.

 bandit14 we used netcat to enter the password of our current user that was sotred in "/etc/bandit_pass/bandit_14". We used " cat " to see the password then "nc localhost 30000" and entered the password we found. For localhost we can also type 127.0.0.1 as well. We get in return password for next level.
    
 bandit15 we need to use 'openssl' to connect to local host 30001. We are using 'openssl s_client -connect localhost:30001' and then we enter the passwrod from the current user. If the password was introduced correct the reply will be with the password for the next level.

 bandit16 we are going to use 'nmap' to listen for open ports in the range 31000-32000. "nmap -sV -T4 -p 31000-32000 localhost"We found port 31790 with ssl/unknown. We are going to try and connect tot the port with "openssl s_client --connect localhost:31790" and we are shown a RSA PRIVATE KEY. We copy it and paste it in a new folder that we will make in /tmp . The new file that is stored in the /tmp will change it's permissions "chmod 400 private.key" then we will try login in to bandit17 using it "ssh -p 2220 bandit17:localhost -i private.key"

 bandit17 we found to files that we compare with 'diff' and the '> dqojmkjdo1jw1odwjo' will be the output difference that is the password for bandit18. 

 bandi18 we where kicked out when we log in. So we simply add -t and location to acces a shell. Command used "ssh -p 2220 bandit18@bandit.labs.overthewire.org -t "/bin/sh" ". Then 'whoami' to check who we are, 'ls' to see available files, it showd readme that we simply open with 'cat'

 bandi19 we have a file on the desktop that we need to check uid. We use "./bandit20-do id" to check 'uid', 'gid', 'euid', 'groups' of the people that have access to it. Then we combine with the location of the password from '/etc/bandit_pass' in "./bandit20-do cat /etc/bandit_pass/bandit20" and it will show us the password for the next level.

 bandit20 we need to use two terminals. In first one we are going to use 'echo' and password and set up a listening port using 'nc', port number can be custom. We used command in first terminal " echo 'current_passowrd' | nc -nlvp 1234 " . Then we switch to the second terminal and use the file that is on /home, " ./suconnect 1234". The connection will be established and the password will be send on the first terminal.

 bandit21 we need to investigate the 'cron_job_files' they are stored in '/etc/cron.d'. Once there we use 'cat' to check the file for bandit22. This indicate there is a script running on reboot and the ***** indicates that is executed periodically. They both corelate to a file '/usr/bin/conrjob_bandit22.sh'. We then simply investigate this with 'cat' again and it shows the password for next level.

 bandit22 we are going back to the same '/tmp' location and inspect the next cronjob file for bandit23. This time is a bash script that generates a password in a specific file. For the script to work we must echo and replace $myname with the user we need password for. For this we are going to do " echo 'I am user bandit23' | md5sum | cut -d ' ' -f 1" . The password will be generate in the specific file and the we simply use 'cat' to open this file and see the password.
