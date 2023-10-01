## Over the Wire: Wargames Solution Walkthrough

##### reminders:
- this walktrough will use the ssh command to connect to the server, so you need to install ssh in your machine
- for windows users, you can use git bash to use the ssh command
- for linux users, you can use the terminal to use the ssh command
- for exiting an ssh connection, you can type exit and press enter 

### level 0
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit0@bandit.labs.overthewire.org's password: bandit0
```

### level 0 -> level 1
```bash
# after connecting with the server using ssh, get the readme file in the home directory
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL  # this code will be used for bandit1 ssh

# connect to bandit1
ssh bandit1@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit1@bandit.labs.overthewire.org's password: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL
```

### level 1 -> level 2
```bash
# study about dashed file (create/read/delete)
# so apparently, you need to add a ./ before the filename to read the file
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi # this code will be used for bandit2 ssh

# connect to bandit2
ssh bandit2@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit2@bandit.labs.overthewire.org's password: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi
```

### level 2 -> level 3
```bash
# study about spaces in a file name
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat 'spaces in this filename'
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG # bandit 3 password

# connect to bandit3
ssh bandit3@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit3@bandit.labs.overthewire.org's password: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG
```

### level 3 -> level 4
```bash
# study about hidden files
# to show hidden files you can add -a to ls command to show all the files
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
bandit3@bandit:~/inhere$ cat .hidden
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe # bandit 4 password

# connect to bandit4
ssh bandit4@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit4@bandit.labs.overthewire.org's password: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe
```

### level 4 -> level 5
```bash
# i did a trial and error on opening all the files to see where the password is hidden
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls -a
.  ..  -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ cat ./-file00
�Ű��Bη���b<Q�Ƞ�+V�iO�1�[5{�bandit4@bandit:~/inhere$ cat ./-file01
jmD�B�0D�tQ*��)�A���V �]Ȕl�bandit4@bandit:~/inhere$ cat ./-file02
x(��z��.T26 F8qqlY���v�FN#��'~bandit4@bandit:~/inhere$ cat ./-file03
�E�Q�"�p�
����4�}�]��G�A��u[�/9�bandit4@bandit:~/inhere$ cat ./-file04
�Mrj�S�r_E�,�����G+�h|�+
�=>KQ�bandit4@bandit:~/inhere$ cat ./-file05
2��]o-p8q�츑���D�
                 .~��&ϯ"PT�Ibandit4@bandit:~/inhere$ cat ./-file06
'�cwk^j�������M����;,���co�9bandit4@bandit:~/inhere$ cat ./-file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR # bandit 5 password

# connect to bandit5
ssh bandit5@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit5@bandit.labs.overthewire.org's password: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR
```

### level 5 -> level 6
```bash
# study about the command find all its parameters
# The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable

bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~/inhere$ find -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ^C
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

# connect to bandit6
ssh bandit6@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit6@bandit.labs.overthewire.org's password: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU
```

### level 6 -> level 7
```bash
# study about the the command find and grep together with its parameters

#The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size

# find all files in the root directory that are owned by user bandit7 and filter that using grep to find the password
bandit6@bandit:/$ find / -user bandit7 2>&1 | grep "password"
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:/$ cat /var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S # bandit 7 password

# connect to bandit7
ssh bandit7@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit7@bandit.labs.overthewire.org's password: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S
```

### level 7 -> level 8
```bash
# The password for the next level is stored in the file data.txt next to the word millionth
bandit7@bandit:~$ less data.txt
# type /millionth to search for the word millionth
millionth       TESKZC0XvTetK0S9xNwm25STk5iWrBvP

# connect to bandit8
ssh bandit8@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit8@bandit.labs.overthewire.org's password: TESKZC0XvTetK0S9xNwm25STk5iWrBvP
```

### level 8 -> level 9
```bash
# study the command sort and uniq
# The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

# sort the data.txt file and filter it using uniq -u to show only the unique lines
# uniq command is used to filter out repeated lines from a sorted file
bandit8@bandit:~$ cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t

bandit8@bandit:~$ cat data.txt | sort | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t

# connect to bandit9
ssh bandit9@bandit.labs.overthewire.org -p 2220

# type the password of the ssh connection
bandit9@bandit.labs.overthewire.org's password: EN632PlfYiZbn3PhVK3XOGSlNInNE00t
```

### level 9 -> level 10
```bash

# The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.




```