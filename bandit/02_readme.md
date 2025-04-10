# [Bandit Level 1 → Level 2](https://overthewire.org/wargames/bandit/bandit2.html)

## Goal
The password for the next level is stored in a file called - located in the home directory.

## Theory
Best file naming conventions for linux.
1. Never use spaces.
2. I prefer lowercase and use `_` as delimiter.
3. I use capitals to ensure important files like README stay at the top of directory listings.
4. No symbols or special characters.

## Solution
1. Login to bandit1 using `ssh bandit1@bandit.labs.overthewire.org -p 2220` and using the password found in the last level.
2. With the `ls` command, we can see a file called `-` in the home directory.
3. Simply using `cat` on this file doesnt work because command options start with a `-` and therefore the shell expects an option and will not open the file.
4. Solution 1. Use the command `cat -- -`. The `--` denote that there are no more options after this.
5. Solution 2. Use the command `cat ./-`.  
