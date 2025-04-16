# [Bandit Level 25 → Level 26](https://overthewire.org/wargames/bandit/bandit26.html)

## Goal
Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

## Theory
`more` command is used to display files which are very long and therefore do not fit properly on the console.

## Solution
1. First check what type of shell bandit26 uses. This is stored in the `/etc/passwd` file.
```
bandit25@bandit:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```
2. Check, using `cat`, what is in the file `/usr/bin/showtext`.
```
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

exec more ~/text.txt
exit 0
```
3. This script opens a file called `text.txt` with the `more` command.
4. We also find a sshkey for bandit26. Copy this key to ssh into bandit26.
```
bandit25@bandit:~$ ls
bandit26.sshkey
```
5. Use `ssh` command with `-i` flag and pass the sshkey to login into bandit26 as we have done before for other levels.
6. When you try to login into bandit26, you get the following response:
```
$ ssh -i bandit26.sshkey bandit26@localhost
...
  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to bandit.labs.overthewire.org closed.
```
7. Connection closes because the script in `/usr/bin/showtext` gets executed and we are thrown out immediately.
8. Probably because `text.txt` is too short and therefore doesnt need long to display it.
9. If we make the terminal window smaller, `more` will go into command mode. Then press 'v' key to go into vim.
10. You can pass several commands within `vim` to start the shell and retrive the password. See documentation [here](https://vimdoc.sourceforge.net/htmldoc/starting.html).
11. `:shell` will start the shell. However, the default shell in this task is of no use to us.
12. Therefore, first change the shell using `:set shell=/bin/bash` and then use `:shell`. Now you should have something familier.
13. Retrive the password using:
```
bandit26@bandit:~$ cat /etc/bandit\_pass/bandit26
s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
```
