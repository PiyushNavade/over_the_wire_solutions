# [Bandit Level 11 → Level 12](https://overthewire.org/wargames/bandit/bandit12.html)

## Goal
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

## Theory
The `tr` command.
The `tr` command reads a byte stream from standard input (stdin), translates or deletes characters, then writes the result to the standard output (stdout).
It is a very powerful command. With it, you can:
1. Convert lowercase to uppercase.
2. Perform basic find and replace operations.
3. Remove repeated instances of a character.
4. Delete specific characters.

## Solution
1. First we read the data.txt file.
```
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```
2. The file contains characters rotated by 13 positions. To undo the rotation, use the `tr` command:
```
tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
3. The `tr` command takes input from the data.txt file in this case, so use the 'pipe symbol' to pass the data.txt file.
```
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
