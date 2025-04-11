# [Bandit Level 6 → Level 7](https://overthewire.org/wargames/bandit/bandit7.html)

## Goal
The password for the next level is stored somewhere on the server and has all of the following properties:
1. owned by user bandit7
2. owned by group bandit6
3. 33 bytes in size

## Theory
For this task, we will once again use the `find` command. According to the task, we have use the `-user`, `-group` and `-size` option with it.

## Solution
1. The task says that the file is located somewhere on the server.
2. We start in the directory `/home/bandit6`, therefore use `cd..` twice to get back in the root.
3. Use `find . -type f -size 33c -user bandit7 -group bandit6` to search on all files. This command will return a bunch of files but most of them we cant access. Eg.
```
find: ‘./root’: Permission denied
find: ‘./proc/tty/driver’: Permission denied
find: ‘./proc/2018360/task/2018360/fdinfo/6’: No such file or directory
find: ‘./proc/2018360/fdinfo/5’: No such file or directory
find: ‘./boot/lost+found’: Permission denied
find: ‘./boot/efi’: Permission denied
find: ‘./etc/polkit-1/rules.d’: Permission denied
```
4. One way is to just scroll past all the permission denied messages to find the correct file.
5. Another way is to omit the permission denied messages. For this use:
```
bandit6@bandit:/$ find . -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
./var/lib/dpkg/info/bandit7.password
```
6. Now we see the file which matches all our criterias and is accessible.
7. `cat` into it and read the password.
