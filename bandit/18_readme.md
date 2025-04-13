# [Bandit Level 17 → Level 18](https://overthewire.org/wargames/bandit/bandit18.html)

## Goal
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new.

## Theory
This task is very straightforward. Use the `diff` command to see the difference between two files.
Both files password.new and password.old contain several passwords, with only one different which is what we want.

## Solution
1. Use the following command.
```
bandit17@bandit:~$ diff passwords.old passwords.new
42c42
< C6XNBdYOkgt5ARXESMKWWOUwBeaIQZ0Y
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```
2. The new password is the second password, since I used password.new as the second argument.
3. Alternate solution. `sort` both the files togethere and then find the unique, `uniq -u`, lines. To find which is the new password, use `grep` on the password.new file.
```
bandit17@bandit:~$ sort passwords.old passwords.new | uniq -u
C6XNBdYOkgt5ARXESMKWWOUwBeaIQZ0Y
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
bandit17@bandit:~$ cat passwords.new | grep C6XNBdYOkgt5ARXESMKWWOUwBeaIQZ0Y
bandit17@bandit:~$ cat passwords.new | grep x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```
