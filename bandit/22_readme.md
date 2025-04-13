# [Bandit Level 21 → Level 22](https://overthewire.org/wargames/bandit/bandit22.html)

## Goal
A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

## Theory - `cron`
A cron job is a Linux command used for scheduling tasks to be executed sometime in the future. This is normally used to schedule a job that is executed periodically – for example, to send out a notice every morning.

## Solution
1. `cd` to `/etc/cron.d/` and use `ls -la` to see all cron jobs.
```
bandit21@bandit:~$ cd /etc/cron.d/
bandit21@bandit:/etc/cron.d$ ls -la
total 48
drwxr-xr-x   2 root root  4096 Apr 10 14:24 .
drwxr-xr-x 121 root root 12288 Apr 10 14:24 ..
-rw-r--r--   1 root root   123 Apr 10 14:16 clean_tmp
-rw-r--r--   1 root root   120 Apr 10 14:23 cronjob_bandit22
-rw-r--r--   1 root root   122 Apr 10 14:23 cronjob_bandit23
-rw-r--r--   1 root root   120 Apr 10 14:23 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-rwx------   1 root root    52 Apr 10 14:24 otw-tmp-dir
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat
```
2. Since we want the password for bandit22, use `cat` to check that particular job.
```
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
3. This cronjob runs the `/usr/bin/cronjob_bandit22.sh` file as bandit22 user. We need to take a look at this file.
```
bandit21@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
4. This file creates a file in the ’tmp’ folder and gives read permission to everyone (indicated by the last 4). Then it copies the input of the bandit22 password file into the newly created file.
5. So the password is in the tmp file.
```
bandit21@bandit:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```
