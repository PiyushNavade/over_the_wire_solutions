# [Bandit Level 8 → Level 9](https://overthewire.org/wargames/bandit/bandit9.html)

## Goal
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once.

## Theory
The file data.txt contains a bunch of possible passwords. Every line has one. We need to find the one password which is unique and not repeated.
1. The `sort` command.
   Used to print the output of a file in given order.
   - `-n` option used to sort numeric values.
   - `-r` option used to sort in reverse.
   - `-k [number]` option used to sort a particular column.
   - `-u` option used to eliminate duplicates.
   - can be used with other commands like `ls` to sort files in a given folder.
2. The `uniq` command.
   An easy way to filter text files and remove duplicate lines from a stream of data.
   - `-d` option used to print duplicate files.
   - `-D` option used to print all instances of the duplicates.
   - `-c` option prefixes each line with the number of times it appears in the file and prints it to the screen.
   - `-u` option removes the duplicates.

## Solution
The solution is a simple one line command once you understand the above two commands. We will use three commands separated by the pipe symbol.
1. Use `cat data.txt | sort | uniq -u`. The `cat` commands prints the result of sorting the file and finding the unique element in it.
```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```
