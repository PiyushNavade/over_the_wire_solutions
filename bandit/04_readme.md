# [Bandit Level 3 → Level 4](https://overthewire.org/wargames/bandit/bandit4.html)

## Goal
The password for the next level is stored in a hidden file in the inhere directory.

## Theory
With the `ls` command without any options, hidden files are not displayed.
To display the hidden files, use the -a option.
File names which are preceded by dots \(...\) are hidden files.

## Solution
1. Login as bandit3.
2. Use the command `cd inhere` to change the workng directory.
3. Use the command `ls -a`. The file is called '...Hiding-From-You'.
4. Use the command `cat ...Hiding-From-You` to get the password to bandit4.
