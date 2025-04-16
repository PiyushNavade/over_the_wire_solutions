# [Bandit Level 22 → Level 23](https://overthewire.org/wargames/bandit/bandit23.html)

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

## Theory
This task introduces `varibales` in bash scripting.
1. A variable is like a container for a value.
2. To declare a variable in bash scripting, use `variable_name = variable_value`. 
3. It is possible to save the output of a command in a variable with the following syntax: `var_name=$(command)`.
4. To access the value of an existing variable, use `$var_name`.

## Solution
1. Similar to the last task, run `cat etc/cron.d/cronjob_bandit23`
```
bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
2. Now look into the script that is running.
```
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
3. `myname=$(whoami)` indicates that the varibale `myname` stores the output of command `$(whoami)`. Since this script will run as bandit23, the varibale `myname` will have bandit23 in it.
4. `mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)` indicates that the varibale `mytarget` stores the output of command `$(echo I am user $myname | md5sum | cut -d ' ' -f 1)`.
5. The last line `cat /etc/bandit_pass/$myname > /tmp/$mytarget` indicates that the password for bandit23 is copied to `/tmp/$mytarget`. We need to find what the varibale `mytarget` contains.
6. For this run the command `echo I am user $myname | md5sum | cut -d ' ' -f 1` and replace `$myname` with bandit23.
```
bandit22@bandit:~$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```
7. Now we know the location of the password. Use `cat`.
```
bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
