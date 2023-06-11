   This is the Walktrough of Bandit

  For first challange bandit0 -> bandit1 :
  We log on using command 
  ssh -p 2220 bandit0@bandit.labs.overthewire.org  
  The user and pw was provided on website.
  We found a file 'readme' that we opend with 'cat readme'. Inside it contained
  the PW for the next level.

  We log on using command ssh -p 2220 bandit1@bandit.labs.overthewire.org
  There is a '-' file. It can be read by using 'head ./-', found the pw for next level

#We are not going to show the command to login anymore, should be self explanitory from now on how to login. I am going to write only about the method used to solve the challange

  For bandit2 we have "space in the filename" file that we open with 
   'cat' and we find the password

  For bandit3 we have a ".hidden" file. We used 
   'cat ./.hidden' to find the password

  For bandit4 we used
   "find -type f | xargs file | grep text" 
 that will display the file that contains ASCII text. Then we open the file using "cat ./-file" and it shows us the pwd

  For bandit5 we used
 "find -type f -size 1033c -non -executable -exec ls -lh {} +" 
 in order to find a human-readable, 1033 bytes in size, not executable file. Then we open it with "cat"

  For bandit6 we used 
 "find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null"
that fits the fallowing criteria : owned by user bandit7, owned by group bandit6, 33 bytes in size. It shows the full path to the file that we are looking for and then we open the file with "cat file_path" and we get the pwd for next level

   For bandit7 we used
 "grep "millionth" data.txt" 
to find pwd next to the word in the file

  For bandit8 we first used 
 'grep -o '.*' data.txt' 
to extract each line. Then we added 
 ' | sort'
Finally we used the 'uniq -u' option to display the unique lines that occur only once. Final command was 
   "grep -o '.*' data.txt | sort | uniq -u"
and we found the password
  
  For bandit9 we combined 'strings' and 'grep' in
 "strings data.txt | grep "^==.*$" " 
and it showed the password. The "^==.*$" pattern matches the lines that started with == followed by any number of chars. This pattern is used to find lines preceded by several '=' chars

  For bandit10 we simpy used 
 "base64 -d"
that decodes the file and shows the password for next level 

  For bandit11 we rotated by 13 positions, with the 'tr' command. We used to decode
 "tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt"
and it prints out the password

  For bandit12 we firs went to the file "/home/bandit13" where we found a ssh private key file call "sshkey.private". Then we keep using "file" to inspect the type of data, then we keep extracting it based on what type of 'data' is. Also we need to "mv" file as ".g". Ex: mv data8.bin data8.bin.gz . We keep doing it so until we have a ASCII text file.
