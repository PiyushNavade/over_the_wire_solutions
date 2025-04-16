# [Bandit Level 27 → Level 28](https://overthewire.org/wargames/bandit/bandit28.html)

## Goal
There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27.
Clone the repository and find the password for the next level.

## Theory
This level introduces `git`. [Git](https://git-scm.com/) is a version control tool. In this level we will use the following git command:
1. `git clone` - to copy an existing git repository on your local machine.

## Solution
1. First create a temp folder to work for this task since the home folder doesnt allow copying the repo.
2. Use `git clone` to download the repo via port 2220. When asked, enter the password for bandit27.
```
bandit27@bandit:/tmp/tmp.3asPoNhq9C$ git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
```
3. See what you have downloaded.
```
bandit27@bandit:/tmp/tmp.3asPoNhq9C$ ls -la
total 364
drwx------    3 bandit27 bandit27   4096 Apr 16 12:46 .
drwxrwx-wt 8103 root     root     360448 Apr 16 12:47 ..
drwxrwxr-x    3 bandit27 bandit27   4096 Apr 16 12:46 repo
bandit27@bandit:/tmp/tmp.3asPoNhq9C$ cd repo
bandit27@bandit:/tmp/tmp.3asPoNhq9C/repo$ ls -la
total 16
drwxrwxr-x 3 bandit27 bandit27 4096 Apr 16 12:46 .
drwx------ 3 bandit27 bandit27 4096 Apr 16 12:46 ..
drwxrwxr-x 8 bandit27 bandit27 4096 Apr 16 12:46 .git
-rw-rw-r-- 1 bandit27 bandit27   68 Apr 16 12:46 README
```
4. The `.git` directory contains all information that is required for version control. It contains information about commits, the remote repository address, a log and more.
5. Only other file is `README`. Open it. 
```
bandit27@bandit:/tmp/tmp.3asPoNhq9C/repo$ cat README
The password to the next level is: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
```
