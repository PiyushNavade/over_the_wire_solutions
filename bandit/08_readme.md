# [Bandit Level 7 → Level 8](https://overthewire.org/wargames/bandit/bandit8.html)

## Goal
The password for the next level is stored in the file data.txt next to the word millionth.

## Theory
The file data.txt contains two columns. First column has random words and the second has password.
We need to find the row which has the word 'millionth' in the first column and the password will be in the second column.

## Solution
1. This task is a straightforward use of `grep`.
```
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
