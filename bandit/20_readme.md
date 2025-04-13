# [Bandit Level 19 → Level 20](https://overthewire.org/wargames/bandit/bandit20.html)

## Goal
To gain access to the next level, you should use the setuid binary in the homedirectory. 
Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

## Theory
1. A setuid binary is an executable file in Unix-like systems that is granted a special permission allowing it to run with the privileges of its owner, regardless of who is running it.
2. Suid is a special linux permission. It will replace the 'x' of the user permission.
3. To give a binary suid permissions the following command needs to be used: `chmod u+s [filename]`.

## Solution
1. As the task directs, I executed the file, bandit20-do, and got the following response.
```
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```
2. The file executes another command `id` as bandit20. This is very helpful because now we can simply read bandit20's password.
```
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```  
