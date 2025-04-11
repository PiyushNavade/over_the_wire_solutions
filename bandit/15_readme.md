# [Bandit Level 14 → Level 15](https://overthewire.org/wargames/bandit/bandit15.html)

## Goal
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

## Theory
The `nc` command is a versatile networking utility for reading and writing data between networks. In this level, there is a service running on the 'local host' which returns 
the password for the next level after we give the password for the current level.
Basic syntax: `nc [options] [hostname] [port]`
Popular options used with the `nc` command:
1. `-l`	Listen mode. Sets up a listening socket.
2. `-p`	Local port. Specifies the target port number to connect to.
3. `-z`	Zero-I/O mode. Scans and detects open ports on the target host.
4. `-e`	Execute. Runs a specified command after establishing a connection.
5. `-c` Shell command. Executes a command as a single argument to the shell.

## Solution
1. We first need the password for the current user, bandit14. According to the last level, it is located in `/etc/bandit_pass/bandit14`.
2. Get the password of bandit14.
```
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```
3. Use the `nc` command with port option 30000 and localhost as the hostname. And once prompted, enter the password for bandit14 and get the password for bandit15.
```
bandit14@bandit:~$ nc localhost 30000
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```
