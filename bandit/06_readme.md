# [Bandit Level 5 → Level 6](https://overthewire.org/wargames/bandit/bandit6.html)

## Goal
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
1. human-readable
2. 1033 bytes in size
3. not executable

## Theory
There are many ways to solve this problem. I have used `find` and `file` commands.
First with the `find` command, I list all the files which are 1033 bytes in size and are not executable.
Then with the `file` command, I confirm that these are human-readable.

## Solution
1. Login to bandit5.
2. Use `cd inhere` to change the directory.
3. There are many directories. We have to find one which contains a file which is human-readable AND 1033 bytes in size AND not executable.
```
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
```
4. Using the `find` command. Theres only one file that matches the criteria.
```
bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable
./maybehere07/.file2
```
5. Using the `file` command on this file to see if it is human readable.
```
bandit5@bandit:~/inhere$ file ./maybehere07/.file2
./maybehere07/.file2: ASCII text, with very long lines (1000)
```
6. It is indeed readable. So use `cat` to read it.
