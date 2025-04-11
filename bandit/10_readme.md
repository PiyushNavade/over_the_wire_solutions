# [Bandit Level 9 → Level 10](https://overthewire.org/wargames/bandit/bandit10.html)

## Goal
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

## Theory
1. The `strings` command.
   Used to extract readable strings from a binary file.
   - The `-n` flag allows you to specify the minimum string length to be printed.
   - The `-t` flag allows you to print the offset within the file before each string.
   - The `-f` flag is useful when you’re processing multiple files. It precedes each string with the name of the file where it was found.

## Solution
1. `strings` command is useful when you have to find human-readable strings in a binary file.
2. Simpy using `strings data.txt` will return several lines which are all human readable.
3. To find the lines which are preceded by '=', use `grep` on the output of `strings`.
```
bandit9@bandit:~$ strings data.txt | grep ===
========== the
========== password{k
=========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
````
