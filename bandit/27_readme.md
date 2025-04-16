# [Bandit Level 26 → Level 27](https://overthewire.org/wargames/bandit/bandit27.html)

## Goal
Good job getting a shell! Now hurry and grab the password for bandit27!

## Solution
1. Use `ls` to check what files exist on bandit26.
```
bandit26@bandit:~$ ls
bandit27-do  text.txt
```
2. The `text.txt` was used for the last level. Now we see a file called `bandit27-do`. Lets execute it to see what happens.
```
bandit26@bandit:~$ ./bandit27-do 
Run a command as another user.
  Example: ./bandit27-do id
```
3. As seen in level 20, it just runs a command as another user. You can easily get the password as bandit27.
```
bandit26@bandit:~$ ./bandit27-do cat /etc/bandit\_pass/bandit27
3ba3118a22e93127a4ed485be72ef5ea
```
