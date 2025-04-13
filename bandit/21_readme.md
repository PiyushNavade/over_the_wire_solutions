# [Bandit Level 20 → Level 21](https://overthewire.org/wargames/bandit/bandit21.html)

## Goal
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. 
It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

## Theory
In this task, we have to create a server. I have used `nc` commmand for this with the following flags.
1. `-l` the server is in the listening mode.
2. `-p` the server is created on a specified port.
3. `&` the command ends with an '&', it will send the process in the background. 

## Solution
1. I find a file called 'suconnect' and I try to run it.
```
bandit20@bandit:~$ ls -la
total 36
drwxr-xr-x  2 root     root      4096 Apr 10 14:23 .
drwxr-xr-x 70 root     root      4096 Apr 10 14:24 ..
-rw-r--r--  1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--  1 root     root      3771 Mar 31  2024 .bashrc
-rw-r--r--  1 root     root       807 Mar 31  2024 .profile
-rwsr-x---  1 bandit21 bandit20 15608 Apr 10 14:23 suconnect
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
bandit20@bandit:~$
```
2. Now we need to open a server and connect to it using `./suconnect [portnumber]`. We also have to make sure that when we connect to it, our server should transmit the password for the current level.
```
bandit20@bandit:~$ echo '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' | nc -l -p 2222 &
[2] 543636
bandit20@bandit:~$ ./suconnect 2222
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
[2]-  Done                    echo '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO' | nc -l -p 2222
bandit20@bandit:~$
```
